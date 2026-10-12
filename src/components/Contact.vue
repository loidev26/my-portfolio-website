<script setup>
	import { ref, onMounted, onBeforeMount } from 'vue';
	import { Notyf } from 'notyf';
	import 'notyf/notyf.min.css';

	const notyf = new Notyf();

	const WEB3FORMS_API_KEY = 'YOUR_WEB3FORMS_API_KEY';

	const subject = "New message from Portfolio Contact Form";

	const name = ref("");
	const email = ref("");
	const message = ref("");
	const isLoading = ref(false);

	const submitForm = async () => {
		
		if(!recaptchaToken.value) {
			notyf.error("Please verify that you are not a robot.");
			return;
		}

		isLoading.value = true;
		
		try {

			const response = await fetch("https://api.web3forms.com/submit", {
				method: "POST",
				headers: {
					"Content-Type": "application/json",
					Accept: "application/json"
				},

				body: JSON.stringify({
					access_key: WEB3FORMS_API_KEY,
					name: name.value,
					email: email.value,
					message: message.value,
					subject: subject,
					"g-recaptcha-response": recaptchaToken.value
				})
			})

			const result = await response.json();

			if (result.success) {
				console.log(result);
				isLoading.value = false;
				notyf.success("Message Sent!")
			}
		} catch (e) {
			console.log(e);
			isLoading.value = false;
			notyf.error("Failed to send message. Please try again.");
		} finally {
			resetRecaptcha();
		}
	}
</script>
<template>
	<section id="contact" class="my-5 py-5">
		<div class="container bg-custom">
			<div class="row">
				<div class="col-md-12 col-lg-6 p-5">

					<h3>
						Get In Touch
					</h3>
					<p>
						Currently looking for new opportunities in full-stack engineering. Let's
						discuss your project.
					</p>
					<div class="d-flex">
						<div class="bi bi-envelope fs-1 p-2 mt-1 me-3">
						</div>
						<div class="">
							<p class="mt-3 mb-0">Email</p>
							<p class="mb-0">loisaamper07@gmail.com</p>
						</div>
					</div>
					<div class="d-flex">
						<div class="bi bi-geo-alt fs-1 p-2 mt-1 me-3">
						</div>
						<div class="">
							<p class="mt-3 mb-0">location</p>
							<p class="mb-0">SJDM, BULACAN</p>
						</div>
					</div>
				</div>
				<div class="col-md-12 col-lg-6">
					<form class="w-100 p-5">
						<div class="d-md-flex gap-2">
				            <div class="mb-3 flex-grow-1">
				                <label for="name" class="form-label">Name</label>
				                <input type="text" class="form-control" id="name" placeholder="John Doe">
				            </div>

				            <div class="mb-3 flex-grow-1">
				                <label for="email" class="form-label">Email</label>
				                <input type="text" class="form-control" id="email" placeholder="johndoe@example.com">
				            </div>
				        </div>
					  
					  	<div class="mb-3">
						  	<label for="message" class="form-label">Message</label>
						  	<textarea class="form-control" id="message" rows="7" placeholder="Type here your message..."></textarea>
						</div>
						<button type="submit" class="btn btn-dark w-100 btn-submit">Send Message</button>
					</form>
				</div>
			</div>
		</div>
	</section>
</template>