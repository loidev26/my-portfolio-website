<template>
    <section id="projects" class="my-5 py-5">
           <div class="container">

               <h2 class="text-center">Featured Projects</h2>
               <hr class="custom-hr mx-auto" />

               <div
                   v-for="(group, index) in chunkedProjects"
                   :key="index"
                   class="row g-4 mt-5"
               >
                   <div
                       v-for="project in group"
                       :key="project.id"
                       class="col-12 col-md-6 col-lg-4"
                   >
                       <ProjectCard :project="project" />
                   </div>
               </div>

           </div>
       </section>
</template>

<script setup>
    import { computed } from 'vue';
    import ProjectCard from './ProjectCard.vue';
    import projects from '../data/projects.json';

    const chunkSize = 3;

    const chunkedProjects = computed(() => {

        const chunks = [];

        for(let i = 0; i < projects.length; i += chunkSize) {
           
            chunks.push(projects.slice(i, i + chunkSize));
        }

        return chunks;
    })
</script>