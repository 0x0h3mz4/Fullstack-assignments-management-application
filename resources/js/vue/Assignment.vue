<template>
    <div v-show="hide">
        <li class="list-group-item border-0 d-flex align-items-center ps-0">
            <div class="row input-group">
                <div class="col-1">
                    <input class="form-check-input ms-3" type="checkbox" @change="updateCheck()"
                        v-model="assignment.completed" />
                </div>
                <div class="col-7">
                    <span :class="[assignment.completed ? 'completed' : 'float-start', 'assignmentText']">{{
                        assignment.name }}</span>
                </div>

                <div class="col-4">
                    <button @click="removeItem()" class=" float-end text-danger me-5">
                        <font-awesome-icon icon="trash" />
                    </button>
                </div>
            </div>

        </li>
    </div>
</template>
<style>
.completed {
    text-decoration: line-through;
    color: gray;
}

.trash {
    color: brown;
    background-color: white;
}
</style>
<script setup>
import axios from 'axios';
import { ref } from 'vue'
let hide = ref("true")
const props = defineProps(['assignment'])
const emit = defineEmits(['assignmentchanged'])
function removeItem() {
    axios.delete('api/assignment/' + props.assignment.id)
        .then(
            Response => {
                emit('assignmentchanged');
            }
        )
        .catch(Error => console.log(Error))
}
function updateCheck() {
    let assignmentHelper = props.assignment
    console.log(assignmentHelper)
    axios.put('api/assignment/' + props.assignment.id, {
        assignment: assignmentHelper
    })
        .then(Response => {
            if (Response.status == 200) {
                emit('assignmentchanged');
            }
        })
        .catch(error => {
            console.log(error);
        })
}
</script>