<template>
  <div>
    <form>
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
  }),
  mounted() {
    fetch(API_URL).then((response) => response.json()).then((result) => {
      console.log(result);
      this.messages = result;
    });
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
