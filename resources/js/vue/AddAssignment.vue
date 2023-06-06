<template>
    <div>
        <form>
            <div class="form-group mx-sm-3 mb-2">
                <label for="exampleInputEmail1">Add an assignment</label>
                <div class="input-group">
                    <input type="email" class="form-control" id="exampleInputEmail1" v-model="nameAssignment">
                    <div class="input-group-btn">
                        <font-awesome-icon icon="plus-square" class="p-3" size="2x"
                            :class="[nameAssignment ? 'active' : 'inactive', 'plus']" @click="addAssignment" />
                    </div>

                </div>
            </div>
        </form>
    </div>
</template>
<style>
.active {
    color: #4BB543;
}

.inactive {
    color: #000;
}
</style>
<script setup>
import { ref } from 'vue'
import axios from 'axios'

let nameAssignment = ref("")
const emit = defineEmits(['reloadList'])
function addAssignment() {
    let assname = nameAssignment.value
    if (nameAssignment.value = '') {
        return;
    }
    axios.post('api/assignment/store',
        {
            assignment: {
                name: assname
            }
        })
        .then(Response => {

            if (Response.status == 201) {
                emit('reloadList');
            }
        })
        .catch(error => { console.log(error.response.data) })
}

</script>
