<template>
    <section id="record">
        <div id="record-header">
            <div class="record-header-icons">Take a tour</div>
            <div class="record-header-icons"><i class="fa fa-envelope"></i></div>
            <div class="record-header-icons"><i class="fa fa-bell"></i></div>
            <div class="record-header-icons user-image">
                
            </div>
        </div>
        <div class="update-title">
            <h2>Update Patient Medical Records</h2>
            <h6>Click the tabs to view and edit patients medical details</h6>
        </div>
        <div class="record-body">
            <form>
                <div class="record-title records-title">{{xRayTitle}}</div>
                <div class="x-ray-container">
                    <span v-for="records in xRayData" :key="records.id" class="x-ray">
                        <input type="checkbox" v-bind:value='records.title' v-model="checkBox1"  id="chest" />
                        <label for="chest">{{records.title}}</label>
                    </span>
                </div>
                <hr />
                <div class="record-title ultra-title">{{ultraSoundScanTitle}}</div>
                <div class="x-ray-container ultraSoundScan">
                    <span v-for="scan in ultraSoundScan" :key="scan.id" class="x-ray">
                        <input type="checkbox" v-bind:value='scan.title' v-model="checkBox2" id="chest" />
                        <label for="chest">{{scan.title}}</label>
                    </span>
                </div>
                <hr />
                <div class="select-wrapper">
                    <div class="ct-scan">
                        <div><label>CT Scan</label></div>
                        <select class="select">
                                <option>Specify</option>
                        </select>
                    </div>
                    <div class="mri">
                        <div><label>MRI</label></div>
                        <select class="select">
                                <option>Specify</option>
                        </select>
                    </div>
                </div>     
                <div class="button-wrapper"><button type="button" @click="submitRecord">Save and Send</button></div>           
            </form>
        </div>
        <div v-bind:id="togglePopup">Successfully Submitted</div>
    </section>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Record',
  data() {
    return {
        xRayData: [],
        ultraSoundScan: [],
        xRayTitle: "",
        ultraSoundScanTitle: "",
        checkBox1: [],
        checkBox2: [],
        togglePopup: "hidePopUp",
        name_Id: 0
        
    }
  },
  beforeMount() {
    this.getToken()
  },
  methods: {

    //The below code generates the dynaminc Token from the Login Endpoint
    async getToken() {
        const requestOptions = {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ email: "tester@kompletecare.com", password: 'password' })
    };
    fetch("https://testdrive.kompletecare.com/api/login", requestOptions)
    .then(response => response.json())
    .then(data => (this.getData(data.data.token)));
    },
    //The below code is supposed to use the generated Token to fetch the API Records but it is returning 'message: unauthorized'  
    async getData(val = "") {
        const requestOption = {
            method: 'GET',
            headers: { 
                'Content-Type': 'application/json',
                'Authorization': 'Bearer ' + val
            }
        };
     fetch("https://testdrive.kompletecare.com/api/investigations", requestOption)
    .then(response => response.json())
    .then(data => {
        (this.xRayData = data.data[0].investigations);
        (this.ultraSoundScan = data.data[1].investigations);
        (this.ultraSoundScanTitle = data.data[1].title);
        (this.xRayTitle = data.data[0].title);

    });
    },
    firePopup() {
        this.togglePopup = 'showPopUp';
        setTimeout(this.hidePopupHandler, 3000);
    },
    hidePopupHandler() {
         this.togglePopup = 'hidePopUp';
    }
  }

});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#record {
    width: 65%;  
    position: relative;
    padding-bottom: 40px;
    background-color: #f2f2f2;
}
#record-header {
    display: flex;
    align-items: center;
    justify-content: flex-end;
    padding: 40px 30px;
}
.record-header-icons {
    padding-right: 30px;
}
.update-title {
    padding-left: 50px;
}
.update-title h2,.update-title h6 {
    color: rgb(2, 2, 141);
    font-weight: 400;
    margin-bottom: 15px;
}
.user-image img {
    width: 35.5px;
    border-radius: 50%; 
}
.user-image {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background-color: #ffffff;
}
.record-body {
    background-color: #ffffff;
    padding: 30px 20px 30px 40px;
    margin: 0px 50px;
}
.x-ray-container,.select-wrapper {
    display: flex;
    flex-wrap: wrap;
    align-content: center;
}
.x-ray {
    display: inline-block;
    width: 25%;
    height: 45px;
    font-size: 9pt;
    font-weight: 600;
}
.x-ray input[type="checkbox"] {
    margin-right: 5px;
}
.ultraSoundScan {
    margin-top: 30px;
}
.record-title {
     color: rgb(2, 2, 141);
}
.records-title {
    padding: 20px 0px;
}
.ultra-title {
    padding-top: 20px;
}
.select {
    width: 80%;
    height: 30px;
}
.ct-scan,.mri {
    width: 50%;
    font-size: 9pt;
    font-weight: 600;
    padding-top: 20px;
}
.ct-scan label,.mri label {
    display: inline-block;
    padding-bottom: 6px;
}  
form button {
    background-color: rgb(2, 2, 141);
    color: #ffffff;
    padding: 10px;
    display: inline-block;
    margin-top: 30px;
    text-align: right;
} 
form hr {
    color: rgba(2, 2, 141, 0.1);
}
.button-wrapper {
    display: flex;
    align-items: flex-end;
    justify-content: flex-end;
    padding: 0px 20px 0px 40px;
}
#showPopUp {
    position: absolute;
    top: 50%;
    left: 40%;
    background-color: rgba(2, 2, 141, 0.9);
    color: #ffffff;
    padding: 20px;
    visibility: visible;
}
#hidePopUp {
    position: absolute;
    top: 50%;
    left: 40%;
    background-color: rgba(2, 2, 141, 0.9);
    color: #ffffff;
    padding: 20px;
    visibility: hidden;
}
@media only screen and (min-width: 200px)  and (max-width: 801px) { 
    #record {
        width: 100%;  
    }
    .record-body {
        padding: 30px 10px 30px 10px;
        margin: 0px 25px 0px 18px;
    }
.x-ray {
    display: block;
    width: 100%;
}
.update-title h2 {
    font-size: 12.5pt;
}
    
}


</style>
