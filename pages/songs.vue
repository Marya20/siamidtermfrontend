<template>
    <div>
        <NavBar />
        <EditSong :song="selectedSong" />
        <DeleteSong :song="selectedSong" @onDeleted="getAll"/>
        <div class="container">
            <h1>
                Songs
                <SongsModalEntry class="float-right" @onAdd="getAll"/>
            </h1>

            <table class="table table-bordered table-stripped shadow">
                <thead>
                    <tr class="bg-info text-white">
                        <th>Song Name</th>
                        <th>Writer</th>
                        <th>Release Date</th>
                        <th>Singer</th>
                        <th>Genre</th>
                        <th>&nbsp;</th>
                        <th>&nbsp;</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="song in songs" :key="song.id">
                        <td>{{song.name}}</td>
                        <td>{{song.writer}}</td>
                        <td>{{song.release_date}}</td>
                        <td>{{song.singer}}</td>
                        <td>{{song.genre}}</td>
                        
                        
                        <td>
                            <b-button @click="onEdit(song)" variant="info" size="sm">
                                Edit
                            </b-button>
                        </td>
                        <td>
                            <b-button @click="onDelete(song)" variant="danger" size="sm">
                                Delete
                            </b-button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
export default {
    
    data() {
        return {
            songs: [],
            selectedSong: {}
        }
    },
    methods: {
        async getAll() {
            await this.$axios.get('https://lentrix.tk/daileen/api/songs')
            .then((res)=>{
                if(res.status==200) {
                    this.songs =res.data
                }
            })
        },
        onEdit(selectedSong) {
            this.selectedSong = selectedSong;
            this.$bvModal.show('editSong')
        },
        onDelete(selectedSong) {
            this.selectedSong = selectedSong;
            this.$bvModal.show('deleteSong')
        }
    },
    created() {
        this.getAll()
    }
}
</script>