<template>
  <section id="dashboard">
        <div class="menu active">
          <i class="fa fa-tachometer" aria-hidden="true"></i> 
          <span>Dashboard</span>
      </div>
      <div class="menu">
          <i class="fa fa-user" aria-hidden="true"></i>
          <span>Profile</span>
      </div>
      <div class="menu">
          <i class="fa fa-dropbox"></i>
          <span class="services">Services <ul>
              <a href="#"><li>Service A</li></a>
              <a href="#"><li>Service B</li></a>
              <a href="#"><li>Service C</li></a>
          </ul></span>
          <i class="fa fa-chevron-down"></i>
      </div>
      <div class="menu">
          <i class="fa fa-file"></i>
          <span>Medical Records</span>
      </div>
      <div class="menu">
          <i class="fa fa-medkit"></i>
          <span>Care Wallet</span>
      </div>
      <div class="menu">
          <i class="fa fa-comment"></i>
          <span>Messages</span>
      </div>
      <div class="menu">
          <i class="fa fa-rocket" aria-hidden="true"></i>
          <span>Resources</span>
      </div>
      <hr />
      <div class="menu">
          <i class="fa fa-cog" aria-hidden="true"></i>
          <span>Account Settings</span>
      </div>
      <div class="menu">
          <i class="fa fa-phone" aria-hidden="true"></i>
          <span>Contact Support</span>
      </div>
      <div class="menu">
          <i class="fa fa-sign-out" aria-hidden="true"></i>
          <span>Logout</span>
      </div>    
  </section>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Dashboard',

});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#dashboard {
    width: 250px;
    height: 500px;
    background-color: #ffffff;
}
.menu {
    padding: 15px;
    display: flex;
    font-size: 10.5pt;
    position: relative;
    align-items: center;
    color: rgb(2, 2, 141);
}
.menu span {
    padding-left: 15px;
}
.menu:hover,.menu ul li:hover {
    background-color: rgb(2, 2, 141);
    color: #ffffff;
}
.services {
    padding-right: 110px; 
}
.menu ul {
    position: absolute;
    width: 100%;
    left: 0%;
    top: 48px;
    z-index: 1;
    list-style: none;
    display: none;
    background-color: #f2f2f2;
}
.menu:hover ul {
    display: block;
}
.menu ul li {
    padding: 15px;
}
.menu ul a {
    text-decoration: none;
    color: #000000;
}
.active {
    background-color: rgb(2, 2, 141);
    color: #ffffff;
}
#dashboard hr {
  color: rgba(2, 2, 141, 0.1);
}
@media only screen and (min-width: 200px)  and (max-width: 801px) { 
    #dashboard {
        width: 40px;
        height: 600px;
    }
    
}

</style>
