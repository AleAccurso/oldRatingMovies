<template>
  <div>
    <table class="table">
      <thead>
        <tr>
          <th scope="col">ID</th>
          <th scope="col">Name</th>
          <th scope="col">Email</th>
          <th scope="col">Admin</th>
          <th scope="col">Update</th>
          <th scope="col">Delete</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in getterUsers" :key="user.id">
          <td>{{ user._id }}</td>
          <td>{{ user.name }}</td>
          <td>{{ user.email }}</td>
          <td>{{ user.isAdmin }}</td>
          <td><nuxt-link :to="{ name: 'updateUser-id', params: { userId: user._id }}"><button>
            <svg style="width:24px;height:24px;color:#22d157;" viewBox="0 0 24 24">
              <path fill="currentColor" d="M21.7,13.35L20.7,14.35L18.65,12.3L19.65,11.3C19.86,11.09 20.21,11.09 20.42,11.3L21.7,12.58C21.91,12.79 21.91,13.14 21.7,13.35M12,18.94L18.06,12.88L20.11,14.93L14.06,21H12V18.94M12,14C7.58,14 4,15.79 4,18V20H10V18.11L14,14.11C13.34,14.03 12.67,14 12,14M12,4A4,4 0 0,0 8,8A4,4 0 0,0 12,12A4,4 0 0,0 16,8A4,4 0 0,0 12,4Z" />
            </svg>
            </button></nuxt-link></td>
          <td>
            <button @click="deleteUser(user._id)">
            <svg style="width:24px;height:24px;color:#ad0545" viewBox="0 0 24 24">
              <path fill="currentColor" d="M9,3V4H4V6H5V19A2,2 0 0,0 7,21H17A2,2 0 0,0 19,19V6H20V4H15V3H9M9,8H11V17H9V8M13,8H15V17H13V8Z" />
            </svg>
          </button></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
   data() {
        return {

        }
    },
    computed: {
        getterUsers(){
            return this.$store.getters.getterUsers;
        }
    },
    created(){
      this.getUsers();
    },
    methods: {
        getUsers() {
          this.$store.dispatch('getUsers');
        },
        deleteUser(_id) {
          this.$store.dispatch('deleteUser', _id);
          this.$router.push('/admin/users');
        }

    }
};
</script>

<style>
tr{
  font-family: 'Lato', sans-serif;
  font-weight: 600;
  color: #9042b4;
  font-size: 17px;
}
td{
  color: #fff;
}

</style>
