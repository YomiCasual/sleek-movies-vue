<template>
	<form @submit.prevent="submitForm" class="search-form">
		<input type="text" 
        v-model="searchTerm"
        placeholder="Enter your movie here..." />
		<input type="submit" value="Search" />
	</form>
</template>

<script>
import { ref } from 'vue'
export default {
   setup(props, {emit}) {
       const searchTerm = ref('')

       const submitForm = () => {
           if(searchTerm.value !== "") {
               emit('searchMovie', searchTerm.value)
               searchTerm.value = ""
           }
       }

       return {
           searchTerm,
           submitForm,
           props
       }
   }
};
</script>

<style lang="scss">
.search-form {
	padding: 2rem 3rem;
	display: flex;
	flex-direction: column;
	justify-content: center;
    align-items: center;

	input {
		background-color: none;
		outline: none;
		border: none;
	

	&[type='text'] {
		color: #496583;
		width: 100%;
		background-color: white;
		font-size: 20px;
		padding: 0.5rem 1rem;
        border-radius: 8px;
        border: 1px solid #496583;
        margin-bottom: 1rem;
	}

    &:focus {
        box-shadow: 0px 3px 6px rgba(0,0,0,0.2);
    }

    &[type="submit"] {
        background-color:  #42b883;
        color: white;
        font-size: 16px;
        padding: 0.5rem 2rem;
        max-width: 300px;
        font-weight: bold;
        cursor: pointer;
        text-transform: uppercase;
        border-radius: 4px;
        transition: 0.5s all ease;

        &:hover, &:focus {
            background-color:  #1d8556;
        }
    }
}
}
</style>
