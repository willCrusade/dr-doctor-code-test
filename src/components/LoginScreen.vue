
<template>
	<main class="card card-large has-info-section">
		<aside class="card-info card-info--dark">
			<header class="card-info-header">
				<img class="card-logo" src="/src/assets/drdoctor-company-logo.svg"/>
			</header>

			<section class="card-info-body">
				<h2 class="text-primary">Healthcare has changed.</h2>
				<p class="text-white">Clinicians all over the UK use the DrDoctor Patient Engagement Platform to make data driven decisions, activate patients through self-booking and provide remote care.</p>
			</section>

			<footer class="card-info-footer">
				<article class="testimonial">
					testimonials here
				</article>
			</footer>
		</aside>

		<section class="card-body relative">
			<LoadingOverlay v-if="isLoading" />
				<FormHandler
					v-if="! hasPatientData"
					:form-data="loginForm"
					@submit="onLoginFormSubmit"
				>
					<template v-slot:description>
						<h3>Log in</h3>
						<p>Don't have an account? <a href="#/">Sign up</a></p>
					</template>

					<template v-slot:fields>
						<TextInput
							label="Surname"
							name="surname"
							maxLength="50"
							required
							v-model="loginForm.lastName"
						/>

						<DateInput
							label="Date of Birth"
							name="date-of-birth"
							required
							v-model="loginForm.dateOfBirth"
						/>

						<TextInput
							label="Postcode"
							name="postcode"
							required
							v-model="loginForm.postCode"
						/>

					</template>

					<template v-slot:submit>
						<input
							type="submit"
							class="btn btn-primary btn-large rounded btn-submit"
							value="Get your patient info"
						/>
					</template>
				</FormHandler>

				<FormHandler
					v-else
					@submit="onOneTimeCodeAccepted"
				>
					<template v-slot:description>
						<div class="form-description">
							<h3>How would you like us to contact you?</h3>
						</div>
					</template>

					<template v-slot:fields>
						<div class="flex">
							<RadioInput
								name="contact-method"
								v-model="contactMethod"
								value="Email"
								:label="patientData.email"
								:checked="contactMethodIs('email')"
							/>

							<RadioInput
								name="contact-method"
								v-model="contactMethod"
								value="Mobile"
								:label="patientData.mobileNumber"
								:checked="contactMethodIs('mobileNumber')"
							/>

							<RadioInput
								name="contact-method"
								v-model="contactMethod"
								value="Landline"
								:label="patientData.phoneNumber"
								:checked="contactMethodIs('phoneNumber')"
							/>


						</div>

						<button
							type="button"
							class="btn btn-primary btn-large rounded btn-submit"
							@click="requestOneTimeCode"
						>
							Get your one time access code
						</button>
					</template>

					<template v-slot:submit>
						<div v-if="showOneTimeCodeField">
							<OneTimeCode
								@complete="onOneTimeCodeAccepted"
							/>
						</div>

					</template>
				</FormHandler>
		</section>
	</main>
</template>

<script>
	import TextInput from "./form/TextInput.vue";
	import DateInput from "./form/DateInput.vue";
	import FormHandler from "./form/FormHandler.vue";
	import LoadingOverlay from "./global/LoadingOverlay.vue";
	import RadioInput from "./form/RadioInput.vue";
	import OneTimeCode from "./form/OneTimeCode.vue";

	export default {
		name: 'LoginScreen',
		components: {
			RadioInput,
			FormHandler,
			TextInput,
			DateInput,
			LoadingOverlay,
			OneTimeCode
		},
		data() {
			return {
				loginForm: {
					lastName: '',
					dateOfBirth: '',
					postCode: '',
				},
				isLoading: false,
				patientData: {},
				contactMethod: '',
				showOneTimeCodeField: false,
			}
		},
		computed: {
			hasPatientData() {
				return Object.keys(this.patientData).length;
			}
		},
		methods: {
			async onLoginFormSubmit(){
				this.isLoading = true;
				const patientRequest = await fetch(`${ import.meta.env.VITE_API_BASE_URL }/e5b51cdf-42e7-41ed-ac58-af600f8db770`);
				const patientData = await patientRequest.json();

				// faking load time for the sake of the demo due to the response being instant
				setTimeout(() => {
					this.onSuccessfulPatientRequest(patientData);
				}, 2000)
			},
			onSuccessfulPatientRequest(patientData) {
				this.isLoading = false;
				this.patientData = patientData.patient;

				this.contactMethod = this.patientData.email;
			},
			onOneTimeCodeAccepted() {

			},
			requestOneTimeCode() {
				this.isLoading = true;

				setTimeout(() => {
					this.showOneTimeCodeField = true;
					this.isLoading = false;
				}, 1000);
				// faking for code test

			},
			contactMethodIs(method) {
				return this.contactMethod === this.patientData[method];
			}
		}
	}
</script>

<style scoped>
.card-info-body h2{
	margin-bottom: .4rem;
}
</style>
