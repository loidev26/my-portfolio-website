<script setup>
    import { ref, onMounted, onBeforeMount } from "vue";
    import { Notyf } from 'notyf';
    import 'notyf/notyf.min.css';

    const notyf = new Notyf();

    const WEB3FORMS_ACCESS_KEY = "25746edd-2888-4a62-ac1c-c0143e7ef1c7";

    const subject = "New message from Portfolio Contact Form";

    const name = ref("");
    const email = ref("");
    const message = ref("");
    const isLoading =ref(false);

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
                    access_key: WEB3FORMS_ACCESS_KEY,
                    subject: subject,
                    email: email.value,
                    name: name.value,
                    message: message.value
                })
            })

            const result = await response.json();

            if (result.success) {
                console.log(result);
                isLoading.value = false;
                notyf.success("Message Sent!")
            }
        } catch(e) {
            console.log(e);
            isLoading.value = false;
            notyf.error("Failed to send message. Please try again.")
        } finally {
					isLoading.value = false;
					resetRecaptcha();
				}
    }
    const SITE_KEY = '6Lf_mustAAAAACYHb4GmgSDi_B6gitp30I1jCYwo';

    const recaptchaContainer = ref(null);
    const recaptchaWidgetId = ref(null);
    const recaptchaToken = ref('');

    // Callback called by reCAPTCHA when successful
    function onRecaptchaSuccess(token) {
        recaptchaToken.value = token;
    }

    // Callback when expired
    function onRecaptchaExpired() {
        recaptchaToken.value = '';
    }

    // Function to render the reCAPTCHA widget
    function renderRecaptcha() {
        if (!window.grecaptcha) {
            console.error('reCAPTCHA not loaded');
            return;
        }

        recaptchaWidgetId.value = window.grecaptcha.render(recaptchaContainer.value, {
            sitekey: SITE_KEY,
            size: 'normal', // or 'compact'
            callback: onRecaptchaSuccess,
            'expired-callback': onRecaptchaExpired,
        });
    }

    // Function to reset reCAPTCHA
    function resetRecaptcha() {
        if (recaptchaWidgetId.value !== null) {
            window.grecaptcha.reset(recaptchaWidgetId.value);
            recaptchaToken.value = '';
        }
    }

    let interval;

		onMounted(() => {
				interval = setInterval(() => {
						if (window.grecaptcha && window.grecaptcha.render) {
								renderRecaptcha();
								clearInterval(interval);
						}
				}, 100);
		});

		onBeforeUnmount(() => {
				clearInterval(interval);
		});
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
					<form @submit.prevent="submitForm" class="w-100 p-5">
						<div class="d-md-flex gap-2">
				          <div class="mb-3 flex-grow-1">
				                <label for="name" class="form-label">Name</label>
				                <input 
													type="text" 
													class="form-control" 
													id="name" 
													placeholder="John Doe"
													v-model="name">
				            </div>

				            <div class="mb-3 flex-grow-1">
				                <label for="email" class="form-label">Email</label>
				                <input 
													type="text" 
													class="form-control" 
													id="email" 
													placeholder="johndoe@example.com"
													v-model="email">
				            </div>
				        </div>
					  
					  	<div class="mb-3">
								<label for="message" class="form-label">Message</label>
								<textarea
									class="form-control"
									id="message"
									rows="7"
									placeholder="Type here your message..."
									v-model="message"
								></textarea>
							</div>

						<!-- recaptcha checkbox -->
						<div class="d-flex justify-content-end mt-2">
								<div ref="recaptchaContainer"></div>
						</div>

						<button
							type="submit"
							class="submit-btn pl-5 pr-5"
							:disabled="isLoading">
									{{ isLoading ? "Sending..." : "Send Message" }}
						</button>
					</form>
				</div>
			</div>
		</div>
	</section>
</template>