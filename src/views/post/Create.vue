<template>
    <div class="container mt-5">
        <div class="row">
            <div class="col-md-12">
                <div class="card border-0 rounded shadow">
                    <div class="card-body">
                        <h4>TAMBAH USER</h4>
                        <hr>

                        <form @submit.prevent="store">
                            <div class="form-group">
                                <label for="name" class="font-weight-bold">USER</label>
                                <input type="text" class="form-control" v-model="post.name" placeholder="Masukkan Nama User">
                                <!-- validation -->
                                <div v-if="validation.name" class="mt-2 alert alert-danger">
                                    {{ validation.name[0] }}
                                </div>
                            </div>

                            <div class="form-group">
                                <label for="job" class="font-weight-bold">JOB</label>
                                <input type="text" class="form-control" v-model="post.job" placeholder="Masukkan JOB">
                                <!-- validation -->
                                <div v-if="validation.job" class="mt-2 alert alert-danger">
                                    {{ validation.job[0] }}
                                </div>
                            </div>

                             
                            <div class="mt-3">
                            <button type="submit" class="btn btn-primary">SIMPAN</button>
                            </div>
                        </form>                        

                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { reactive, ref } from 'vue'
import { useRouter } from 'vue-router'
import axios from 'axios'

export default {

    setup() {

        //state posts
        const post = reactive({
            user: '',
            job: ''
        })

        //state validation
        const validation = ref([])

        //vue router
        const router = useRouter()

        //method store
        function store() {

            let user   = post.user
            let job = post.job

            axios.post('https://reqres.in/api/users', {
                user: user,
                job: job
            }).then(() => {

                //redirect ke post index
                router.push({
                    name: 'post.index'
                })

            }).catch(error => {
                //assign state validation with error 
                validation.value = error.response.data
            })

        }

        //return
        return {
            post,
            validation,
            router,
            store
        }

    }

}
</script>

<style>
    body{
        background: lightgray;
    }
</style>