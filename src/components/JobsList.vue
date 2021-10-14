<template>
  <div class="list">
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
              <p>{{ lang }}</p>
            </div>
            <div v-for="tool in job.tools" :key="tool" class="languagesAndToolsInfos">
              <p>{{ tool }}</p>
            </div>
          </div>
          
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import data from "@/assets/data/data.json";

export default {
  name: 'JobsList',
  data() {
    return {
      jobs: data,
    }
  }
}
</script>

<style scoped lang="scss">
@import '@/css/vars.scss';

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

.img {
  border-radius: 50%;
  width: 4rem;
  height: 4rem;
  margin: 1.5rem;
}

.infos {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
}

.name{
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
  margin: 0.5rem 0;
  width: 100%;
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

  .img {
    position: relative;
    top: -0.8rem;
    margin: 0 0.5rem;
  }

  .infos {
    width: 100%;
    margin-bottom: 0.5rem;
  }

}

</style>
