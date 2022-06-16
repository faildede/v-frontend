<template> 
  <div> 
    <h1 class="">Products</h1> 
    <div v-if="fetching"> 
      Loading... 
    </div> 
    <div v-else-if="error"> 
      Oh no... {{ error }} 
    </div> 
    <div v-else> 
      <div class="container mx-auto" v-if="data"> 
                  <p class="ml-12 text-4xl leading-10 font-light">{{ data.products_by_id.title }}</p>
        <div class="container bg-white mx-auto mt-12 mb-3 flex w-2/4"> 
          <img class="w-96" :src="'http://38.242.229.113:8055/assets/' + data.products_by_id.image.id" alt="">       
       <div class="mt-12 container p-6 mx-auto" >
          <div class=" ">
            <p>Цвет:</p>
          </div>
       <div class="mt-6 border-t mx-2">
              <p class="mx-auto font-semibold text-lg">Цена:  <span class="font-semibold text-base"> {{ data.products_by_id.price }} $ </span></p>
              <button class="eee my-5 px-7 py-3 text-white rounded-full hover:black-200 block text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 :focus:ring-blue-800" type="button" data-modal-toggle="default-modal"> <i class="fas fa-shopping-cart"></i>  купить</button> 
           
          <p> Описание:<br/> {{ data.products_by_id.description }}</p> 
       </div>
       </div>
        </div> 
      </div> 
    </div> 
    
  </div> 
</template> 
 
<script>
import { useRoute } from "vue-router"; 
import { useQuery, gql } from "@urql/vue"; 
export default { 
  setup() { 
    const route = useRoute(); 
    const getProductQuery = gql` 
      query ($id: ID!) { 
        products_by_id(id: $id) { 
          id 
          title 
          price 
          description 
          image { 
            id 
          } 
        } 
      } 
    `; 
    const getProduct = useQuery({ query: getProductQuery, variables: { id: route.params.id } }); 
    return { 
      fetching: getProduct.fetching, 
      data: getProduct.data, 
      error: getProduct.error, 
    }; 
  }, 
}; 
</script> 
 
<style scoped></style>