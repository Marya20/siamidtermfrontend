
<template>
    <div>

        <b-modal id="editSong" title="Song Entry" ok-title="Save Song" @ok="onSubmit">
           <form action="#" >
                <b-form-group 
                label="Song Name"
                label-for="name"
                >
                <b-form-input id="name" v-model="song.name"  trim></b-form-input>
                </b-form-group>

                 <b-form-group
                label="Writer"
                label-for="writer"
                >
                <b-form-input id="writer" v-model="song.writer"  trim></b-form-input>
                </b-form-group>

                 <b-form-group
                label="Release Date"
                label-for="release_date"
                >
                <b-form-input id="release_date" type="date" v-model="song.release_date"  trim></b-form-input>
                </b-form-group>

                 <b-form-group
                label="Singer"
                label-for="singer"
                >
                <b-form-input id="singer" v-model="song.singer"  trim></b-form-input>
                </b-form-group>

                 <b-form-group 
                label="Genre"
                label-for="genre"
                >
                <b-form-input id="genre"  v-model="song.genre"  trim></b-form-input>
                </b-form-group>

           </form>

        </b-modal>
    </div>
</template>

<script>
export default {
  props:{
      song:{}
  },
   data() {
        return{
            song:{},
                  
        }
    },
  methods:{
        async onSubmit() {
            this.$axios.put('https://lentrix.tk/daileen/api/songs/' + this.song.id, this.song)
            .then((res)=>{
                if(res.status==202) {
                    alert('Updated Successfully!!!')
                }
            })
            .catch((err)=> {
                alert(err.message)
            })
        }
    }
}
</script>