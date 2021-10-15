<template>
  <section>
    <div v-if="filters.length > 0" >
      <div class="filterSection">
        <div>
          <ul class="filters">
            <li class="filter" v-for="(filter, index) in filters" :key="filter">
              <p>{{ filter }}</p>
              <span @click="removeFilter(filter, index)">
                <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-x" width="25" height="25" viewBox="0 0 24 24" stroke-width="2.5" stroke="#ffffff" fill="none" stroke-linecap="round" stroke-linejoin="round">
                  <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
                  <line x1="18" y1="6" x2="6" y2="18" />
                  <line x1="6" y1="6" x2="18" y2="18" />
                </svg>
              </span>
            </li>
          </ul>
        </div>
        <span class="clear" @click="removeAllFilters">Clear</span>
      </div>

      <div>
        <ul v-for="filteredJob in filteredJobsArr" :key="filteredJob.id">
          <li>
            <div 
              class="jobcard"
              v-bind:class="{ featuredJobStyle: filteredJob.featured }"
            >
              <div class="primaryInfos">
                <div class="img">
                  <img 
                    :src="filteredJob.logo" 
                    :alt="'Logo  of '+ filteredJob.company"
                  >
                </div>

                <div class="infos">
                  <h3 class="name">{{ filteredJob.company }}</h3>
                  <span v-if="filteredJob.new === true" class="new">New !</span>
                  <span v-if="filteredJob.featured === true" class="featured">Featured</span>
                  <h3 class="position">{{ filteredJob.position }}</h3>

                  <div class="subInfos">
                    <p>{{ filteredJob.postedAt }}</p>
                    <p>{{ filteredJob.contract }}</p>
                    <p>{{ filteredJob.location }}</p>
                  </div>
                </div>
              </div>
            
              <div class="secondaryInfos">
                <div v-for="lang in filteredJob.languages" :key="lang" class="languagesAndToolsInfos">
                  <p @click="addFilter(lang)">{{ lang }}</p>
                </div>
                <div v-for="tool in filteredJob.tools" :key="tool" class="languagesAndToolsInfos">
                  <p @click="addFilter(tool)">{{ tool }}</p>
                </div>
              </div>
              
            </div>
          </li>
        </ul>
      </div>
    </div>

    <div v-else class="list">
      <ul v-for="job in jobs" :key="job.id">
        <li>
          <div 
            class="jobcard"
            v-bind:class="{ featuredJobStyle: job.featured }"
          >
            <div class="primaryInfos">
              <div class="img">
                <img 
                  :src="job.logo" 
                  :alt="'Logo  of '+ job.company"
                >
              </div>

              <div class="infos">
                <h3 class="name">{{ job.company }}</h3>
                <span v-if="job.new === true" class="new">New !</span>
                <span v-if="job.featured === true" class="featured">Featured</span>
                <h3 class="position">{{ job.position }}</h3>

                <div class="subInfos">
                  <p>{{ job.postedAt }}</p>
                  <p>{{ job.contract }}</p>
                  <p>{{ job.location }}</p>
                </div>
              </div>
            </div>
          
            <div class="secondaryInfos">
              <div v-for="lang in job.languages" :key="lang" class="languagesAndToolsInfos">
                <p @click="addFilter(lang)">{{ lang }}</p>
              </div>
              <div v-for="tool in job.tools" :key="tool" class="languagesAndToolsInfos">
                <p @click="addFilter(tool)">{{ tool }}</p>
              </div>
            </div>
            
          </div>
        </li>
      </ul>
    </div>

  </section>
</template>

<script>
import data from "@/assets/data/data.json";

export default {
  name: 'JobsList',
  data() {
    return {
      jobs: data,
      filters: [],
      filteredJobsArr: [],
    }
  },
  methods: {
    addFilter (filter) {
      // If not already present in array, then add element
      if (!this.filters.includes(filter)) {
        this.filters.push(filter); 
      }

      this.filteredJobsAdd(filter);
    },

    removeFilter (filter, index) {
      // If element = to the received filter, removed it from arr
      if(this.filters[index] === filter) {
        this.filters.splice(index, 1); 
      }

      this.filteredJobsRemove(filter);
    },

    removeAllFilters () {
      this.filters = [];
    },

    // When filters are added to the arr
    filteredJobsAdd(filter) {
      this.jobs.forEach(job => {
        if(job.languages.includes(filter) || job.tools.includes(filter)) {
          this.filteredJobsArr.push(job); 
        }
      });
      // console.log(this.filteredJobsArr);
    },

    // When filters are removed from the arr
    filteredJobsRemove(filter) {
      this.jobs.forEach(job => {
        if(job.languages.includes(filter) || job.tools.includes(filter)) {
          this.filteredJobsArr.pop(job); 
        }
      });
    }
  },
}
</script>

<style scoped lang="scss">
@import '@/css/vars.scss';

.filterSection {
  position: relative;
  background: white;
  box-shadow: 0px 8px 11px -6px rgba(123,142,142,0.67);
  -webkit-box-shadow: 0px 8px 11px -6px rgba(123,142,142,0.67);
  -moz-box-shadow: 0px 8px 11px -6px rgba(123,142,142,0.67);
  border-radius: 5px;
  top: -3.5rem;
  width: 80%;
  margin: 1.3rem auto;
  padding: 1rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.filters {
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;
  align-items: center;
}

.filter {
  margin: 0.5rem;
  background: $Background;
  color: $Primary;
  font-weight: $FontWeightBold;
  border-radius: 3px;
  width: fit-content;
  display: flex;
  align-items: center;
}

.filter p {
  padding: 0.5rem;
}

.filter span {
  background: $Primary;
  color: white;
  padding: 0.3rem 0.5rem;
  border-radius: 3px;
}

.filter span:hover {
  background: $VeryDark;
  cursor: pointer;
}


.clear {
  color: $Primary;
  font-weight: $FontWeightBold;
}

.clear:hover {
  cursor: pointer;
  text-decoration: underline;
}

/* LIST OF JOBS */

.list {
  margin: 4rem 0;
}

.jobcard {
  box-shadow: 0px 8px 11px -6px rgba(123,142,142,0.67);
  -webkit-box-shadow: 0px 8px 11px -6px rgba(123,142,142,0.67);
  -moz-box-shadow: 0px 8px 11px -6px rgba(123,142,142,0.67);
  border-radius: 5px;
  background: white;
  margin: 1rem;
  display: flex;
  justify-content: space-between;
  width: 80%;
  margin: 1.3rem auto;
}

.featuredJobStyle {
  border-left: $Primary solid 5px;
}

.primaryInfos {
  width: 50%;
  display: flex;
  align-items: center;
}

.secondaryInfos {
  width: 45%;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  padding-right: 1rem;
}

.img img {
  border-radius: 50%;
  width: 5rem;
  height: 5rem;
  margin: 1.5rem;
}

.infos {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
}

.name {
  font-weight: $FontWeightBold;
  color: $Primary;
  margin-right: 0.5rem;
}

.new, .featured {
  color: white;
  padding: 0.5rem 0.5rem 0.3rem ;
  border-radius: 30px;
  text-transform: uppercase;
  font-weight: $FontWeightBold;
  margin-right: 0.5rem;
}

.new {
  background: $Primary;
}

.featured {
  background: $VeryDark;
}

.position {
  font-weight: $FontWeightBold;
  font-size: $FontSize * 1.3;
  margin: 1rem 0;
  width: 100%;
}

.position:hover {
  color: $Primary;
  cursor: pointer;
}


.subInfos {
  margin: 0.5rem 0;
  color: $Dark;
  display: flex;
}

.subInfos p:nth-child(1)::after {
  padding: 0.5rem;
  content: "·";
}

.subInfos p:nth-child(2)::after {
  padding: 0.5rem;
  content: "·";
}

.languagesAndToolsInfos p {
  margin: 0 0.5rem;
  background: $Background;
  color: $Primary;
  font-weight: $FontWeightBold;
  padding: 0.5rem 0.5rem 0.3rem ;
  border-radius: 3px;
}

.languagesAndToolsInfos p:hover {
  cursor: pointer;
  background: $Primary;
  color: $Background;
}

/* Small screen */
@media only screen and (max-width: 1440px) {
  .jobcard {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    margin: 4rem auto;
  }

  .primaryInfos {
    width: 80%;
    margin: 0 auto;
    padding: 0 1rem ;
    flex-wrap: wrap;
  }

  .secondaryInfos {
    width: 80%;
    margin: 0 auto;
    justify-content: flex-start;
    padding: 1rem 0;
    border-top: 1px solid $Dark;
  }

  .img img {
    position: relative;
    top: -2rem;
    margin: 0rem;
  }

  .infos {
    width: 100%;
    margin-bottom: 0.5rem;
  }

}

</style>
