<template>
  <div>
    <form @submit.prevent="submitBoard">
      <div class="form-group">
        <label for="username">Username</label>
        <input v-model="message.username" type="text" class="form-control" id="username" required>
      </div>
      <div class="form-group">
        <label for="subject">Subject</label>
        <input v-model="message.subject" type="text" class="form-control" id="subject"
        placeholder="Enter a subject" required>
      </div>
      <div class="form-group">
        <label for="content">Content</label>
        <textarea v-model="message.content" class="form-control" id="content" rows="3"></textarea>
      </div>
      <div class="form-group">
        <label for="imageURL">imageURL</label>
        <input v-model="message.imageURL" type="URL" class="form-control" id="imageURL"
        placeholder="Enter an imageURL">
      </div>
    </form>
    <button type="submit" class="btn btn-outline-danger">Submit</button>
    <div class="list-unstyled"  v-for="message in messages" :key="message._id">
      <li class="media">
        <img v-if="message.imageURL" :src="message.imageURL" class="mr-3" :alt="message.subject">
        <div class="media-body">
          <h5 class="mt-0 mb-1">{{message.username}} | {{message.subject}}</h5>
          {{message.message}}
        </div>
      </li>
      <hr>
    </div>
  </div>
</template>

<script>
const API_URL = 'http://localhost:5000/messages';

export default {
  name: 'Home',
  data: () => ({
    messages: [],
    message: {
      username: 'Anonymous',
      subject: '',
      content: '',
      imageURL: '',
    },
  }),
  mounted() {
    fetch(API_URL).then((response) => response.json()).then((result) => {
      console.log(result);
      this.messages = result;
    });
  },
  methods: {
    submitBoard() {
      console.log(this.message);
    },
  },
};
</script>

<style>
hr {
  border-top: 1px solid gray;
}

img {
  max-width: 300px;
  height: auto;
}
</style>
