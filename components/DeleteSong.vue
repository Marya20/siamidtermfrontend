<template>
    <div>
        <b-modal id="deleteSong" title="Song Entry" ok-title="Delete Song" @ok="onDelete" ok-variant="danger">
            Are you sure you want to delete this song<br> {{song.name}} by {{song.singer}}? <br>
            
        </b-modal>
    </div>
</template>
<script>
export default {
  props:{
      song:{}
  },
  methods:{
        async onDelete() {
            this.$axios.delete('https://lentrix.tk/daileen/api/songs/' + this.song.id)
            .then((res)=>{
                if(res.status==202) {
                    alert('Song deleted')
                    this.$emit('onDeleted')
                }
            })
        }
    }
}
</script>





