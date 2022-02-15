<script setup>
import { computed, defineProps, toRefs } from "vue";

const props = defineProps(["user"]);

const { user } = toRefs(props);

const location = computed(() => {
  const lat = user.value.location?.coordinates.latitude;
  const lng = user.value.location?.coordinates.longitude;

  return `https://maps.google.com/?q=${lat},${lng}`;
});

const address = computed(() => {
  const { street, city, state, postcode } = user.value.location;

  return `${street.number} ${street.name}, ${city}, ${state} - ${postcode}`;
});

const dob = computed(() => {
  const date = new Date(user.value.dob.date);
  const months = [
    "Jan",
    "Feb",
    "Mar",
    "Apr",
    "May",
    "Jun",
    "Jul",
    "Aug",
    "Sep",
    "Oct",
    "Nov",
    "Dec",
  ];
  return `${date.getDate()} ${months[date.getMonth()]} ${date.getFullYear()}`;
});
</script>

<template>
  <div class="card" v-if="user.name">
    <img class="avatar" :src="user.picture.medium" alt="thumbnail" />

    <div class="flex">
      <div>
        <div class="title">
          <div>
            <h2 v-if="user.gender === 'male'">&#9794;</h2>
            <h2 v-else>&#9792;</h2>
          </div>
          &nbsp;
          <h2>
            {{ `${user.name.title}. ${user.name.first} ${user.name.last}` }}
          </h2>
        </div>
        <p v-if="user.id.value" class="over-text">
          {{ user.id.name }} : {{ user.id.value }}
        </p>
        <div class="over-text">{{ address }}</div>
      </div>

      <div>
        <h5>{{ dob }}</h5>
        <h5>{{ user.dob.age }} years old</h5>
      </div>
    </div>

    <br />

    <div class="flex">
      <a :href="`mailto:${user.email}`">{{ user.email }}</a>
      <a :href="`tel:${user.phone}`">{{ user.phone }}</a>
    </div>

    <br />

    <div class="flex">
      <a :href="location" target="_blank">Locate me</a>
      <p class="over-text">
        Member since {{ new Date(user.registered.date).getFullYear() }}
      </p>
    </div>
  </div>
  <div class="footer">
    <p>Made by</p>
    <a href="https://www.twitter.com/lightyaer">@lightyaer</a>
  </div>
</template>

<style scoped>
h2,
h3,
h4,
h5,
p,
a {
  margin: 0;
}

a {
  text-decoration: none;
  color: #0052d4;
}

a:hover {
  text-decoration: underline;
}

.avatar {
  border-radius: 50%;
  position: absolute;
  top: -1rem;
  left: 50%;
  transform: translateX(-50%) translateY(-30%);
  width: 4rem;
}

.title {
  display: flex;
}

.card {
  background-color: whitesmoke;
  padding: 2rem 2rem 1rem 2rem;
  border: 1px solid #363636;
  position: relative;
  width: 30rem;
  margin: 15rem auto;
  border-radius: 1rem;
  box-shadow: #32325d3f 0 1.875rem 3.75rem -0.75rem inset,
    #0000004c 0 1.125rem 2.25rem -1.125rem inset;
}

.flex {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

@media only screen and (max-width: 600px) {
  .card {
    width: 70%;
    padding: 2rem 2rem 1rem 2rem;
  }

  .flex {
    flex-direction: column;
    text-align: center;
  }

  .title {
    justify-content: center;
  }
}

@media only screen and (max-width: 300px) {
  a {
    font-size: 0.8rem;
  }

  .card {
    margin: 6rem auto;
  }
}

.over-text {
  font-size: 0.8rem;
}

.footer {
  color: whitesmoke;
  position: absolute;
  bottom: 2rem;
  width: 100vw;
  text-align: center;
}

.footer a {
  color: whitesmoke;
}
</style>
