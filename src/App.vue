<template>
  <div class="container">
    <div class="row">
      <div class="col-sm">
        <p>Twitter Icon</p>
      </div>
      <div class="col-sm">
        <ul>
          <li>            
            <ul>
              <li style="list-style-type: none" v-for="el in database" v-bind:key="el.id">
                <div class="card">
                  <div class="card-body">
                    UserId: {{el.userId}} <br>
                    Tweet: {{el.message}} <br>
                    <button @click="UpdateTweetLikes(el)">Likes: {{el.likes}}</button> | shares: {{el.shares}} <br>
                    <button @click="DeleteTweet(el.id)">Delete Tweet</button>
                  </div>
                </div>
                <br>
              </li>
            </ul>              
          </li>
        </ul>
        <button @click="ct = true" v-if="ct == false">Create Tweet</button>
        <button @click="ct = false" v-if="ct == true">Cancel</button>
        <div class="card" v-if="ct">
          <div class="card-body">
            <p>Please enter the following info</p>
            <input type="number" placeholder="User ID" v-bind="dbCreateUI">
            <input type="text" placeholder="Your tweet here" v-bind="dbCreateT">
          </div>
        </div>
        <button @click="CreateTweet(dbCreateUI, dbCreateT)" v-if="ct == true">Submit</button>
      </div>
      
      <div class="col-sm">

      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'


export default {
  name: 'App',
    components: {

    },

  data: () => {
    return {
      database: [],
      dbCreateUI: undefined,
      dbCreateT: undefined,
      ct: false,
    }
  },

  computed: {

  },

  methods: {
    CreateTweet() {
      axios.post('https://localhost:7136/api/TweetController', {UserId: 2, Message: "asdf"}).then(response => {
        console.log(response)
        if(response.status == 200){
          console.log("Success, tweet created")
        } else {
          console.log("Failure to create tweet")
        }
      })
    },

    UpdateTweetLikes(el) {
      axios.post(`https://localhost:7136/api/TweetController/${el.id}`).then(response => {
        console.log(response)
      })
    },

    DeleteTweet(id) {
      console.log(id)
      axios.delete(`https://localhost:7136/api/TweetController/${id}`).then(response => { 
        console.log(response)
        console.log(this.database)
        if(response.status == 204){
          console.log("Deletion succeeded")
          for (let index = 0; index < this.database.length; index++) {
            if(this.database[index].id == id){
              this.database.splice(index);
            }
            
          }
        }
      })
    }
  },

  mounted() {
    axios.get('https://localhost:7136/api/TweetController').then(response => {
      console.log(response)
      this.database = response.data
    })

  },
}
</script>

<style>

</style>
