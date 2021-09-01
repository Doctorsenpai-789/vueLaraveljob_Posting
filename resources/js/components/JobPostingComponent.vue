<template>
  <div>
    <h1>JobPosting List</h1>
    <table class="table table-hover">
      <thead>
        <th>Job Name</th>
        <th>Job Description</th>
        <th>Vacants</th>
        <th>Actions</th>
      </thead>
      <tbody>
        <tr v-for= "item in postingList" :key ="item.id">
          <td> {{ item.job_name }} </td>
          <td> {{ item.job_description }}</td>
          <td> {{ item.vacants }}</td>
          <td>
            <button class="btn btn-secondary btn-sm">
              <i class="fa fa-edit"></i>
            </button>
            <button class="btn btn-danger btn-sm">
              <i class="fa fa-trash"></i>
            </button>
          </td>
        </tr>
      </tbody>
      <tfoot>
        <tr>
          <td>
            <div class="form-group">
              <input
                type="text"
                class="form-control"
                placeholder="Input Job Name"
                v-model="form.job_name"
              />
            </div>
          </td>
          <td>
            <div class="form-group">
              <input
                type="text"
                class="form-control"
                placeholder="Input Job Description"
                v-model="form.job_description"
              />
            </div>
          </td>
          <td>
            <div class="form-group">
              <input
                type="number"
                class="form-control"
                placeholder="Input vacants"
                v-model="form.vacants"
              />
            </div>
          </td>
          <td>
            <div class="form-group">
              <button class="btn btn-primary btn-sm" @click="submit">
                <i class="fa fa-plus"></i>
              </button>
            </div>
          </td>
        </tr>
      </tfoot>
    </table>
  </div>
</template>

<script>
export default {
  props:["posting"],
  data() {
    return {
      postingList: this.posting,
      form: {
        job_name: null,
        job_description: null,
        vacants: 0,
      },
    };
  },
  methods: {
    submit() {
     const  vm = this;
      axios
        .post("/job_postings", this.form)
        .then(function (response) {
          vm.postingList.push(response.data.data);
          vm.form.job_name = null;
          vm.form.job_description = null;
          vm.form.vacants = 0;
        
        })
        .catch(function (error) {

         console.log(error)
        });
    },
    delete(iitem , index){
       axios
        .delete(`/job_postings/${item.id}`)
        .then(function (response) {
          vm.postingList.push(response.data.data);
          vm.form.job_name = null;
          vm.form.job_description = null;
          vm.form.vacants = 0;
        
        })
        .catch(function (error) {

         console.log(error)

        });
    }
  },
};
</script>
