<template>
    <div class="row">
      <div class="col-md-12">
        <div class="card">
          <table class="table table-hover">
           <thead>
             <tr class="bg-danger">

               <th>ID </th>
               <th>Name</th>
               <th>Price</th>
               <th>Created At</th>
               <th>Updated At</th>
               <th>Seller Name</th>
             </tr>
          </thead>

          <tbody>
        <tr class="bg-light">
            <tr v-for="product in posts.data">
              <th> {{ product._id }} </th>
              <td> {{ product.name }} </td>
              <td> {{ product.price }} </td>
              <td> {{ product.createdAt }} </td>
              <td> {{ product.updatedAt }} </td>
              <td>Nadine</td>
           </tr>
         </tr>

          </tbody>
        </table>
        </div>
      </div>
      <div>
        <input type="text" v-model = "pro.name"> Name <br>
        <input type="text" v-model ="pro.price" > Price <br>
      <button @click = "create">
        Create!
      </button> <br> <br>

<input type="text" v-model = "pro.id"> ID
<br>

<button @click = "deleteit">
  delete!</button>  <br> <br>

  <input type="text" v-model = "pro.name"> Name <br>
  <input type="text" v-model ="pro.price" > Price <br>
  <input type="text" v-model = "pro.id"> ID <br>
  <button @click= "updateit">
    update! <br>
</button> <br><br>

      </div>
    </div>

</template>

<script>
  import axios from 'axios'

  export default {
    data () {
      return {

        posts: [],
        pro: {
          name: '',
          price: '',
          id: ''
        }
      }
    },
    mounted () {
      var self = this
      axios.get('http://localhost:3000/api/product/getProducts')
    .then(function (res) {
      self.posts = res.data
      console.log('Data: ', res.data)
    })
    .catch(function (error) {
      console.log('Error: ', error)
    })
    },
    methods: {
      create () {
        axios.post('http://localhost:3000/api/product/createProduct', {
          name: this.pro.name,
          price: this.pro.price
        })
      },
      deleteit () {
        axios.delete('http://localhost:3000/api/product/deleteProduct' + '/' + this.pro.id)
      },
      updateit () {
        axios.patch('http://localhost:3000/api/product/updateProduct' + '/' + this.pro.id, {
          name: this.pro.name,
          price: this.pro.price
        })
      }
    }
  }

</script>
<style>

</style>
