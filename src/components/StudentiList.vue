<template>
    <div>
        <StudentSingle v-for="student in studenti" :key="student.id" :student="student"/>
        <hr>
    </div>
</template>

<script>
import StudentSingle from '@/components/StudentSingle.vue';

export default {
    name: 'StudentiList',

    components: {
        StudentSingle
    },

    data() {
        return {
            studenti: []
        }
    },
    
    props: {
        studentiIDs: Array
    },

    watch: {
        studentiIDs(nVal) {
            this.studenti = [];

            nVal.map( obj => {
                fetch(`http://alumni.raf.edu.rs/rs/api/diplomac/${obj.id}`)
                    .then( obj => obj.json())
                    .then( res => this.studenti.push(res));
            });
        }
    },

    mounted() {
        this.studentiIDs.map( obj => {
            fetch(`http://alumni.raf.edu.rs/rs/api/diplomac/${obj.id}`)
                .then( obj => obj.json())
                .then( res => this.studenti.push(res));
        });
    }
}
</script>

<style scoped>
</style>