<template>
  <div class="max-w-screen-sm mx-auto px-4 py-10">
    <!-- App Message -->
    <div v-if="statusMsg || errorMsg" class="mb-10 p-4 rounded-md shadow-md bg-light-grey">
      <p class="text-at-light-green">
        {{statusMsg}}
      </p>
      <p class="text-red-500">
        {{errorMsg}}
      </p>
    </div>
  </div>
</template>

<script>
  import { ref } from 'vue';
  import { supabase } from '@/supabase/init';
  import { useRoute } from 'vue-router';
export default {
  name: "view-workout",
  setup() {
    // Create data / vars
    const data = ref(null)
    const dataLoaded = ref(null)
    const errorMsg = ref(null)
    const statusMsg = ref(null)
    const route = useRoute()

    // Get current Id of route
    const currentId = route.params.workoutId;
    
    // Get workout data
    const getData = async() =>{
      try{
        const {data: workout, error} = await supabase.from('workout').select('*').eq('id',currentId)
        if(error) throw error;
        data.value = workout
        dataLoaded.value = true
      }
      catch(error){
        errorMsg.value = error.message
        setTimeout(()=>{
          errorMsg.value = false
        },5000)
      }
    }

    getData()
    // Delete workout

    // Edit mode

    // Add exercise

    // Delete exercise

    // Update Workout

    return {statusMsg, data, dataLoaded, errorMsg};
  },
};
</script>
