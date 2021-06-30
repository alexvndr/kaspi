<template>
  <div id="app" class="wrapper">
    <div class="header">
      <div></div>
      <div class="title">
        <span class="job">job</span>
        <span class="Agent">Agent</span>
      </div>
      <div class="avatar">
        <img src="@/assets/avatar.svg" width="30px" height="30px">
      </div>
    </div>
    <p class="job-search">job search</p>
    <div class="props">
      <div class="search">
        <img src="@/assets/search.svg" width="15px" height="18px">
        <input type="text" placeholder="Search" v-model="search">
      </div>
      <div class="sort-button">
        <img src="@/assets/sort.svg" width="15px" height="18px">
      </div>
    </div>
    <div class="sort-result">
      <p>Sort by:</p>
      <div class="sorting" @click="toggleArr">
        <p>{{sortBy}}</p>
        <img class="sort-arrow" :class="toMax ? 'up' : 'down'" src="@/assets/arrow.svg">
      </div>
    </div>
    <div class="data" v-for="(job, index) in filteredJobs" :key="index">
      <img :src="getIcon(job.company)" width="40px" height="40px" class="job-img">
      <div class="content">
        <span class="name">{{job.name}}</span>
        <div class="details">
          <div>
            <span>Company:</span>
            <span class="info">{{job.company}}</span>
          </div>
          <div>
            <span>Location:</span>
            <span class="info">{{job.location.city}}, {{job.location.country}}</span>
          </div>
        </div>
        <div class="about">
          <img src="@/assets/clock.svg">
          <span>Posted {{job.postedDaysAgo}} days ago</span>
          <div class="dot"/>
          <img src="@/assets/eye.svg">
          <span>{{job.views}} Views</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import json from './jobs-mock.json';
import Bank from './assets/ssd.svg';
import Lombrisol from './assets/mm.svg';
import CoolHubs from './assets/wd.svg';
import LiveLove from './assets/id.svg';
export default {
  name: 'App',
  data() {
    return {
      jobs: json.jobs,
      sortBy: 'views',
      search: '',
      toMax: false
    }
  },
  computed: {
    filteredJobs() {
        return this.jobs.filter(job => {
            return (
                job.name.toLowerCase().includes(this.search.toLowerCase())
            )
        })
    },
  },
  methods: {
    toggleArr() {
      this.toMax = !this.toMax;
      if(this.toMax) {
        this.jobs.sort(function(a, b) {
          if(a.views > b.views) {
            return 11;
          }
          if(a.views < b.views) {
            return -1;
          }
          return 0;
        })
      }else{
        this.jobs.sort(function(a, b) {
        if(a.views > b.views) {
          return -1;
        }
        if(a.views < b.views) {
          return 1;
        }
        return 0;
      })
      }
    },
    getIcon(title) {
      if(title === 'I&M Bank') {
        return Bank
      }
      if(title === 'Lombrisol') {
        return Lombrisol
      }
      if(title === 'Cool Hubs') {
        return CoolHubs
      }
      if(title === 'Live Love') {
        return LiveLove
      }
      if(title === 'Revolut') {
        return 'https://www.logo.wine/a/logo/Revolut/Revolut-Icon-Black-Logo.wine.svg'
      }
      if(title === 'Improvado') {
        return 'https://www.saashub.com/images/app/service_logos/20/1b07895b2ec1/large.png?1543265891'
      }
      if(title === 'Kaseya') {
        return 'https://www.nexthink.com/wp-content/uploads/2018/04/kaseya-icon.png'
      }
      if(title === 'Orion Innovation') {
        return 'https://pbs.twimg.com/profile_images/1260898355137220608/chxJRsyb.jpg'
      }
      if(title === 'Corning Incorporated') {
        return 'https://pbs.twimg.com/profile_images/1372549434173689863/g4rD_P-B.jpg'
      }
    }
  },
  mounted() {
    this.jobs.sort(function(a, b) {
       if(a.views > b.views) {
         return -1;
       }
       if(a.views < b.views) {
         return 1;
       }
       return 0;
     })
  }
}
</script>

<style>
@font-face {
  font-family: "Roboto";
  src: url("./assets/fonts/Roboto-Light.ttf") format('truetype');
}
@font-face {
  font-family: "Roboto-Medium";
  src: url("./assets/fonts/Roboto-Medium.ttf") format('truetype');
}
@font-face {
  font-family: "Roboto-Regular";
  src: url("./assets/fonts/Roboto-Regular.ttf") format('truetype');
}
body {
  display: flex;
  justify-content: center;
  background: #E5E5E5;
  margin: 0;
}
.wrapper {
  background: #FBFBFB;
  max-width: 420px;
  width: 100%;
  padding: 30px 24px 40px;
  min-height: 100vh;
}
.wrapper .header {
  display: flex;
  justify-content: space-between;
  width: 100%;
  align-items: center;
}
.wrapper .header .title .job {
  letter-spacing: -0.24px;
  font-family: "Roboto-Medium";
  font-style: normal;
  font-weight: 800;
  font-size: 20px;
  line-height: 20px;
  color: #EEAB02;
}
.wrapper .header .title .Agent {
  letter-spacing: -0.24px;
  font-family: "Roboto";
  font-style: italic;
  font-weight: 300;
  font-size: 20px;
  line-height: 20px;
}

.wrapper .job-search {
  text-transform: uppercase;
  color: #636363;
  font-family: "Roboto-Medium";
  font-style: normal;
  font-weight: 800;
  font-size: 16px;
  line-height: 19px;
  margin: 25px 0 16px;
}

.wrapper .props {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 40px;
}
.wrapper .props .search {
  display: flex;
  align-items: center;
  background: #EAEAEA;
  border-radius: 8px;
  padding: 11px 12.5px;
  width: 90%;
}
.wrapper .props .search input {
  outline: none;
  border: none;
  background: #EAEAEA;
  font-family: "Roboto";
  border-radius: 8px;
  font-style: normal;
  font-weight: normal;
  font-size: 14px;
  line-height: 17px;
  color: #636363;
  margin-left: 8px;
}
.wrapper .props .sort-button {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-left: 8px;
  background: #FFC803;
  border-radius: 8px;
  padding: 11px 12.5px;
}
.wrapper .sort-result {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin: 8px 0 30px;
}
.wrapper .sort-result p {
  color: #636363;
  font-family: "Roboto-Medium";
  font-style: normal;
  font-weight: bold;
  font-size: 14px;
  line-height: 17px;
  margin: 0;
}
.wrapper .sort-result .sorting {
  display: flex;
  align-items: center;
}
.wrapper .sort-result .sorting p {
  font-family: "Roboto";
  font-style: normal;
  font-weight: normal;
  font-size: 14px;
  line-height: 16px;
  color: #636363;
  text-transform: capitalize;
  margin: 0;
  margin-right: 10px;
}

.wrapper .sort-result .sorting .up {
  transform: rotateZ(180deg);
  transition: all 0.4s ease;
}
.wrapper .sort-result .sorting .down {
  transform: rotateZ(0deg);
  transition: all 0.4s ease;
}

.wrapper .data {
  display: flex;
  background: #FFFFFF;
  box-shadow: 0px 4px 8px rgba(33, 33, 33, 0.16);
  border-radius: 8px;
  padding: 16px;
  margin-bottom: 16px;
  height: 138px;
}
.wrapper .data .job-img {
  border-radius: 100px;
  margin-right: 16px;
}
.wrapper .data .content {
  display: flex;
  flex-flow: column;
  justify-content: space-between;
  width: 100%;
}
.wrapper .data .content .name {
  font-family: "Roboto-Medium";
  font-style: normal;
  font-weight: bold;
  font-size: 12px;
  line-height: 14px;
  text-transform: uppercase;
  color: #636363;
  min-height: 32px;
}
.wrapper .data .content .details div {
  display: flex;
  justify-content: space-between;
  font-family: "Roboto-Regular";
  font-style: normal;
  font-weight: normal;
  font-size: 12px;
  line-height: 14px;
  color: #636363;
}
.wrapper .data .content .details div:first-child  {
  margin-bottom: 4px;
}
.wrapper .data .content .details div .info {
  text-decoration-line: underline;
  color: #E06D06;
}
.wrapper .data .content .about {
  display: flex;
  align-items: center;
  font-family: "Roboto-Regular";
  font-style: normal;
  font-weight: normal;
  font-size: 12px;
  line-height: 14px;
  color: #636363;
}
.wrapper .data .content .about img {
  margin-right: 8px;
}
.wrapper .data .content .about .dot {
  background: #C4C4C4;
  width: 4px;
  height: 4px;
  border-radius: 100px;
  margin: 0 16px;
}
</style>
