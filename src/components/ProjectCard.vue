<template>
	<div class="card shadow-lg h-100">
	    <img :src="project.image" class="card-img-top p-3" alt="Project Image">

	    <div class="card-body d-flex flex-column">
	        <h5 class="card-title">{{ project.title }}</h5>
	        <p class="card-text">
	        	{{ project.description }}
			</p>
			<div class="d-flex justify-content-center mt-auto flex-wrap flex-sm-nowrap gap-2">
				<a href="#" class="btn btn-live-demo w-100 me-1">Live Demo</a>
				<a href="#" class="btn btn-github w-100 ms-1">Github</a>
			</div>
	    </div>
	</div>
</template>

<script setup>
	import { defineProps } from 'vue';

	defineProps({
		project: Object
	})
</script>