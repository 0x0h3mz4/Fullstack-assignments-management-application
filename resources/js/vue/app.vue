<template>
    <div>
        <section class="vh-100" style="background-color: #3da2c3;">
            <div class="container py-5 h-100">
                <div class="row d-flex justify-content-center align-items-center h-100">
                    <div class="col col-lg-8 col-xl-6">
                        <div class="card rounded-3">
                            <div class="card-body p-4">
                                <p class="mb-2"><span class="h2 me-2">To do List</span> <span
                                        class="badge bg-danger">checklist</span></p>
                                <p class="text-muted pb-2">This is a Laravel & Vue.js project</p>

                                <div>
                                    <AddAssignment v-on:reloadList="getAssignments"></AddAssignment>
                                </div>

                                <div>
                                    <ListAsssignments :assignments="assignments" v-on:reloadList="getAssignments">
                                    </ListAsssignments>
                                </div>

                                <div class="divider d-flex align-items-center my-4">
                                    <p class="text-center mx-3 mb-0" style="color: #a2aab7;">Built by: 0x0h3mz4</p>
                                </div>

                                <ul class="list-group rounded-0 list-group-horizontal justify-content-center pb-2">
                                    <li class="list-group-item border-0 d-flex align-items-center p-0">
                                        <img src="https://media.licdn.com/dms/image/D4E03AQFAO03l8yE3PQ/profile-displayphoto-shrink_100_100/0/1670761932797?e=1691625600&v=beta&t=YIwVyW71scfgHQOaTL8k5qcOFW12HtJsqFPGrQLoEwM"
                                            alt="avatar" class="rounded-circle me-n2" width="45">
                                    </li>
                                </ul>

                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>
    </div>
</template>
<style>
.divider:after,
.divider:before {
    content: "";
    flex: 1;
    height: 1px;
    background: #eee;
}
</style>
<script setup>
import axios from 'axios';
import AddAssignment from './AddAssignment.vue'
import ListAsssignments from './ListAsssignments.vue'
import { ref } from 'vue'
let assignments = ref("")
function getAssignments() {
    axios.get('api/assignments')
        .then(Response => assignments.value = Response.data)
        .catch(error => { console.log(error) })
}
getAssignments()

</script>
