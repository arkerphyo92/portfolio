<script lang="ts">
	import Skills from './ProgressBar.svelte';
	import TypedElement from './TypedElement.svelte';
	import { onMount } from 'svelte';
	import { writable } from 'svelte/store';
	let typedStrings = [
		'Full-Stack Developer',
		'Designer',
		'Python and JavaScript Developer',
		'Project Manager'
	];

	const name = writable('');
	const email = writable('');
	const subject = writable('');
	const message = writable('');
	const errorMessage = writable('');
	const successMessage = writable('');

	async function handleSubmit(event: any) {
		event.preventDefault();
		errorMessage.set('');
		successMessage.set('');

		const formData = {
			user_name: $name,
			user_email: $email,
			message: $message,
			to: 'arker'
		};

		try {
			const response = await fetch('https://api.khantzay.com/api/contact-form', {
				method: 'POST',
				headers: {
					'Content-Type': 'application/json'
				},
				body: JSON.stringify(formData)
			});

			const result = await response.json();

			if (response.ok) {
				successMessage.set('Your message has been sent. Thank you!');
				name.set('');
				email.set('');
				subject.set('');
				message.set('');
			} else {
				errorMessage.set(result.error || 'Failed to send message. Please try again later.');
			}
		} catch (error) {
			errorMessage.set('Failed to send message. Please try again later.');
		}
	}

	onMount(() => {
		// Select all progress bars
		const progressBars = document.querySelectorAll('.progress-bar');

		// Function to add the animation
		function animateProgressBars() {
			progressBars.forEach((bar) => {
				const targetWidth = bar.getAttribute('data-width');
				if (bar instanceof HTMLElement) {
					bar.style.width = targetWidth + '%';
				}
			});
		}

		// Use Intersection Observer to detect when the section is in the viewport
		const observer = new IntersectionObserver(
			(entries, observer) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						animateProgressBars();
						observer.disconnect(); // Stop observing after animation
					}
				});
			},
			{ threshold: 0.5 } // Trigger when 50% of the section is visible
		);

		// Observe the skills section
		const skillsSection = document.querySelector('#skills');
		if (skillsSection) {
			observer.observe(skillsSection);
		}
	});
</script>

<main class="main">
	<!-- Hero Section -->
	<section id="hero" class="hero section dark-background">
		<img src="src/lib/img/arkarphyo.jpg" alt="" data-aos="fade-in" class="" />

		<div class="container" data-aos="fade-up" data-aos-delay="100">
			<h2>ARKAR PHYO</h2>

			<p>
				I'm <span class="typed"
					><TypedElement
						strings={typedStrings}
						typeSpeed={100}
						backSpeed={50}
						backDelay={2000}
						loop={true}
					/></span
				>
			</p>
		</div>
	</section>
	<!-- /Hero Section -->

	<!-- About Section -->
	<section id="about" class="about section">
		<!-- Section Title -->
		<div class="section-title container" data-aos="fade-up">
			<h2>About</h2>
			<p>
				My name is Arkar Phyo and I am working as Full Stack Web Developer. I have been working in
				Software Developement Industry for 7 years as Project Coordinator acting as Project Manager
				and IT Officer.
			</p>
		</div>
		<!-- End Section Title -->

		<div class="container" data-aos="fade-up" data-aos-delay="100">
			<div class="row gy-4 justify-content-center">
				<div class="col-lg-4">
					<img src="src/lib/img/arkarphyo-bio.jpg" class="img-fluid" alt="" />
				</div>
				<div class="col-lg-8 content">
					<h2>Full Stack Web Developer.</h2>
					<p class="fst-italic py-3">This is my Biography</p>
					<div class="row">
						<div class="col-lg-6">
							<ul>
								<li>
									<i class="bi bi-chevron-right"></i> <strong>Birthday:</strong>
									<span>8<sup>th</sup> November 1992</span>
								</li>
								<li>
									<i class="bi bi-chevron-right"></i> <strong>Website:</strong>
									<span>www.akphyo.com</span>
								</li>
								<li>
									<i class="bi bi-chevron-right"></i> <strong>Phone:</strong>
									<span>+66 93 551 662 7</span>
								</li>
								<li>
									<i class="bi bi-chevron-right"></i> <strong>City:</strong>
									<span>Bangkok, Thailand</span>
								</li>
							</ul>
						</div>
						<div class="col-lg-6">
							<ul>
								<li><i class="bi bi-chevron-right"></i> <strong>Age:</strong> <span>32</span></li>
								<li>
									<i class="bi bi-chevron-right"></i> <strong>Email:</strong>
									<span>arkerphyo92@gmail.com</span>
								</li>
								<li>
									<i class="bi bi-chevron-right"></i> <strong>Freelance:</strong>
									<span>Available</span>
								</li>
							</ul>
						</div>
					</div>
				</div>
			</div>
		</div>
	</section>
	<!-- /About Section -->

	<!-- Skills Section -->

	<section id="skills" class="skills section light-background">
		<!-- Section Title -->
		<div class="section-title container" data-aos="fade-up">
			<h2>Skills</h2>
			<p>Necessitatibus eius consequatur ex aliquid fuga eum quidem sint consectetur velit</p>
		</div>
		<!-- End Section Title -->

		<div class="container" data-aos="fade-up" data-aos-delay="100">
			<div class="row skills-content skills-animation">
				<div class="col-lg-6">
					<div class="progress">
						<span class="skill"
							><span>Python (Django, Litestar, Typesense, SQLAlchemy, Alembic, API)</span>
							<i class="val">95%</i></span
						>
						<div class="progress-bar-wrap">
							<div
								class="progress-bar"
								role="progressbar"
								aria-valuenow="95"
								aria-valuemin="0"
								aria-valuemax="100"
								style="width: 0;"
								data-width="95"
							></div>
						</div>
					</div>
					<!-- End Skills Item -->

					<div class="progress">
						<span class="skill"
							><span>TailwindCSS / Bootstrap (HTML/CSS)</span> <i class="val">90%</i></span
						>
						<div class="progress-bar-wrap">
							<div
								class="progress-bar"
								role="progressbar"
								aria-valuenow="90"
								aria-valuemin="0"
								aria-valuemax="100"
								style="width: 0;"
								data-width="90"
							></div>
						</div>
					</div>
					<!-- End Skills Item -->

					<div class="progress">
						<span class="skill"
							><span>Database (PostgreSQL, MYSQL, MSSQL, SQLITE)</span> <i class="val">80%</i></span
						>
						<div class="progress-bar-wrap">
							<div
								class="progress-bar"
								role="progressbar"
								aria-valuenow="80"
								aria-valuemin="0"
								aria-valuemax="100"
								style="width: 0;"
								data-width="80"
							></div>
						</div>
					</div>
					<!-- End Skills Item -->
				</div>

				<div class="col-lg-6">
					<div class="progress">
						<span class="skill"
							><span>JavaScript (ReactJs, SvelteKit, TypeScript)</span> <i class="val">80%</i></span
						>
						<div class="progress-bar-wrap">
							<div
								class="progress-bar"
								role="progressbar"
								aria-valuenow="80"
								aria-valuemin="0"
								aria-valuemax="100"
								style="width: 0;"
								data-width="80"
							></div>
						</div>
					</div>
					<!-- End Skills Item -->

					<div class="progress">
						<span class="skill"><span>WordPress/CMS</span> <i class="val">90%</i></span>
						<div class="progress-bar-wrap">
							<div
								class="progress-bar"
								role="progressbar"
								aria-valuenow="90"
								aria-valuemin="0"
								aria-valuemax="100"
								style="width: 0;"
								data-width="90"
							></div>
						</div>
					</div>
					<!-- End Skills Item -->

					<div class="progress">
						<span class="skill"><span>Docker/ Github</span> <i class="val">75%</i></span>
						<div class="progress-bar-wrap">
							<div
								class="progress-bar"
								role="progressbar"
								aria-valuenow="75"
								aria-valuemin="0"
								aria-valuemax="100"
								style="width: 0;"
								data-width="75"
							></div>
						</div>
					</div>
					<!-- End Skills Item -->
				</div>
			</div>
		</div>
	</section>
	<!-- /Skills Section -->

	<!-- Resume Section -->
	<section id="resume" class="resume section">
		<!-- Section Title -->
		<div class="section-title container" data-aos="fade-up">
			<h2>Resume</h2>
			<p>
				Magnam dolores commodi suscipit. Necessitatibus eius consequatur ex aliquid fuga eum quidem.
				Sit sint consectetur velit. Quisquam quos quisquam cupiditate. Et nemo qui impedit suscipit
				alias ea. Quia fugiat sit in iste officiis commodi quidem hic quas.
			</p>
		</div>
		<!-- End Section Title -->

		<div class="container">
			<div class="row">
				<div class="col-lg-6" data-aos="fade-up" data-aos-delay="100">
					<h3 class="resume-title">Sumary</h3>

					<div class="resume-item pb-0">
						<h4>Brandon Johnson</h4>
						<p>
							<em
								>Innovative and deadline-driven Graphic Designer with 3+ years of experience
								designing and developing user-centered digital/print marketing material from initial
								concept to final, polished deliverable.</em
							>
						</p>
						<ul>
							<li>Portland par 127,Orlando, FL</li>
							<li>(123) 456-7891</li>
							<li>alice.barkley@example.com</li>
						</ul>
					</div>
					<!-- Edn Resume Item -->

					<h3 class="resume-title">Education</h3>
					<div class="resume-item">
						<h4>Project Management Certificate, ICM-PM</h4>
						<h5>2022</h5>
						<p><em>Strategy First University</em></p>
					</div>
					<div class="resume-item">
						<h4>International Business Communication. ICM-IBC UK</h4>
						<h5>2020</h5>
						<p><em>Strategy First University</em></p>
					</div>
					<div class="resume-item">
						<h4>Professional Web Developing Course</h4>
						<h5>2018</h5>
						<p><em>Fairway Technology</em></p>
					</div>
					<div class="resume-item">
						<h4>Advanced Creative Design</h4>
						<h5>2018</h5>
						<p><em>Hexagon – Yangon Bee</em></p>
					</div>
					<div class="resume-item">
						<h4>The Bachelor of Arts: English</h4>
						<h5>2011 - 2013</h5>
						<p><em>Yangon East University</em></p>
					</div>
					<div class="resume-item">
						<h4>Web Essential</h4>
						<h5>2012</h5>
						<p><em>Myanmar World Wide Web Institute</em></p>
					</div>
					<!-- Edn Resume Item -->
				</div>

				<div class="col-lg-6" data-aos="fade-up" data-aos-delay="200">
					<h3 class="resume-title">Professional Experience</h3>
					<div class="resume-item">
						<h4>Full-Stack Web Developer</h4>
						<h5>2024 - Present</h5>
						<p><em>HexCode Tech, Bangkok, Thailand </em></p>
						<ul>
							<li>
								Develop, test, and maintain web applications using Django, Litestar (Python),
								SvelteKit(JS) and ReactJS.
							</li>
							<li>Design and implement robust, scalable, and secure RESTful APIs.</li>
							<li>
								Collaborate with AI developers and other team members to integrate user-facing
								elements with server-side logic.
							</li>
							<li>
								Optimize applications for maximum speed and scalability and Implement security and
								data protection measures.
							</li>
							<li>
								Troubleshoot and debug applications to ensure optimal performance. Participate in
								code reviews and contribute to best practices and coding standards.
							</li>
							<li>
								Stay current with the latest developments and trends in Django, SvelteKit and
								related technologies.
							</li>
						</ul>
					</div>
					<!-- Edn Resume Item -->

					<div class="resume-item">
						<h4>Project Coordinator (Acting as Project Manager)</h4>
						<h5>2022 - 2024</h5>
						<p><em>Myanmar Information Technology, Yangon, Myanmar</em></p>
						<ul>
							<li>
								Collaborated with cross-functional teams to develop software products and deliver
								scoped system modules and functionalities.
							</li>
							<li>
								Managed project planning, resources, and execution to ensure on-time delivery of
								medium to large-scale projects.
							</li>
							<li>
								Led stakeholder meetings, aligned project objectives, and adapted scope as needed to
								meet business goals.
							</li>
							<li>
								Created and presented technical reports and project updates to working groups and
								steering committees. Provided post-delivery consulting and technical support,
								ensuring seamless customer experiences.
							</li>
							<li>
								Monitored project schedules, work hours, and expenditures to optimize
								efficiency.Provide software/system training for customers o Regularly report project
								status through Weekly and Monthly updates. Schedule and facilitate meetings,
								preparing meeting minutes
							</li>
						</ul>
					</div>
					<!-- Edn Resume Item -->
				</div>
			</div>
		</div>
	</section>
	<!-- /Resume Section -->

	<!-- Portfolio Section -->
	<section id="portfolio" class="portfolio section light-background">
		<!-- Section Title -->
		<div class="section-title container" data-aos="fade-up">
			<h2>Portfolio</h2>
			<p>
				Magnam dolores commodi suscipit. Necessitatibus eius consequatur ex aliquid fuga eum quidem.
				Sit sint consectetur velit. Quisquam quos quisquam cupiditate. Et nemo qui impedit suscipit
				alias ea. Quia fugiat sit in iste officiis commodi quidem hic quas.
			</p>
		</div>
		<!-- End Section Title -->

		<div class="container">
			<div
				class="isotope-layout"
				data-default-filter="*"
				data-layout="masonry"
				data-sort="original-order"
			>
				<!-- End Portfolio Filters -->

				<div class="row gy-4 isotope-container" data-aos="fade-up" data-aos-delay="200">
					<div class="col-lg-4 col-md-6 portfolio-item isotope-item filter-app">
						<div class="portfolio-content h-100">
							<img src="src/lib/img/portfolio/Divergent.jpg" class="img-fluid" alt="" />
							<div class="portfolio-info">
								<!-- <h4>App 1</h4> -->
								<p>Lorem ipsum, dolor sit amet consectetur</p>
							</div>
						</div>
					</div>
					<!-- End Portfolio Item -->

					<div class="col-lg-4 col-md-6 portfolio-item isotope-item filter-product">
						<div class="portfolio-content h-100">
							<img src="src/lib/img/portfolio/Fashion153.jpg" class="img-fluid" alt="" />
							<div class="portfolio-info">
								<!-- <h4>Product 1</h4> -->
								<p>Lorem ipsum, dolor sit amet consectetur</p>
							</div>
						</div>
					</div>
					<!-- End Portfolio Item -->

					<div class="col-lg-4 col-md-6 portfolio-item isotope-item filter-branding">
						<div class="portfolio-content h-100">
							<img src="src/lib/img/portfolio/Mega24.jpg" class="img-fluid" alt="" />
							<div class="portfolio-info">
								<!-- <h4>Branding 1</h4> -->
								<p>Lorem ipsum, dolor sit amet consectetur</p>
							</div>
						</div>
					</div>
					<!-- End Portfolio Item -->

					<div class="col-lg-4 col-md-6 portfolio-item isotope-item filter-books">
						<div class="portfolio-content h-100">
							<img src="src/lib/img/portfolio/MMtender.jpg" class="img-fluid" alt="" />
							<div class="portfolio-info">
								<!-- <h4>Books 1</h4> -->
								<p>Lorem ipsum, dolor sit amet consectetur</p>
							</div>
						</div>
					</div>
					<!-- End Portfolio Item -->
				</div>
				<!-- End Portfolio Container -->
			</div>
		</div>
	</section>
	<!-- /Portfolio Section -->

	<!-- Contact Section -->
	<section id="contact" class="contact section">
		<!-- Section Title -->
		<div class="section-title container" data-aos="fade-up">
			<h2>Contact</h2>
			<p>Necessitatibus eius consequatur ex aliquid fuga eum quidem sint consectetur velit</p>
		</div>
		<!-- End Section Title -->

		<div class="container" data-aos="fade-up" data-aos-delay="100">
			<div class="row gy-4">
				<div class="col-lg-5">
					<div class="info-wrap">
						<div class="info-item d-flex" data-aos="fade-up" data-aos-delay="200">
							<i class="bi bi-geo-alt flex-shrink-0"></i>
							<div>
								<h3>Address</h3>
								<p>Hua Mark, Bangkok, Thailand</p>
							</div>
						</div>
						<!-- End Info Item -->

						<div class="info-item d-flex" data-aos="fade-up" data-aos-delay="300">
							<i class="bi bi-telephone flex-shrink-0"></i>
							<div>
								<h3>Call Me</h3>
								<p>+66 93 551 662 7</p>
							</div>
						</div>
						<!-- End Info Item -->

						<div class="info-item d-flex" data-aos="fade-up" data-aos-delay="400">
							<i class="bi bi-envelope flex-shrink-0"></i>
							<div>
								<h3>Email Me</h3>
								<p>arkerphyo92@gmail.com</p>
							</div>
						</div>
						<!-- End Info Item -->

						<!-- <iframe
							src="https://www.google.com/maps/embed?pb=!1m14!1m8!1m3!1d48389.78314118045!2d-74.006138!3d40.710059!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x89c25a22a3bda30d%3A0xb89d1fe6bc499443!2sDowntown%20Conference%20Center!5e0!3m2!1sen!2sus!4v1676961268712!5m2!1sen!2sus"
							frameborder="0"
							style="border:0; width: 100%; height: 270px;"
							allowfullscreen=""
							loading="lazy"
							referrerpolicy="no-referrer-when-downgrade"
						></iframe> -->
					</div>
				</div>

				<div class="col-lg-7">
					<form
						on:submit={handleSubmit}
						class="php-email-form"
						data-aos="fade-up"
						data-aos-delay="200"
					>
						<div class="row gy-4">
							<div class="col-md-6">
								<label for="name-field" class="pb-2">Your Name</label>
								<input
									type="text"
									name="name"
									id="name-field"
									class="form-control"
									bind:value={$name}
								/>
							</div>

							<div class="col-md-6">
								<label for="email-field" class="pb-2">Your Email</label>
								<input
									type="email"
									class="form-control"
									name="email"
									id="email-field"
									bind:value={$email}
								/>
							</div>

							<div class="col-md-12">
								<label for="message-field" class="pb-2">Message</label>
								<textarea
									class="form-control"
									name="message"
									rows="2"
									id="message-field"
									bind:value={$message}
								></textarea>
							</div>

							<div class="col-md-12 text-center">
								<div class="loading">Loading</div>
								<div class="error-message">{$errorMessage}</div>
								<div class="sent-message">{$successMessage}</div>

								<button type="submit">Send Message</button>
							</div>
						</div>
					</form>
				</div>
				<!-- End Contact Form -->
			</div>
		</div>
	</section>
	<!-- /Contact Section -->
</main>

<footer id="footer" class="footer position-relative light-background">
	<div class="container">
		<div class="copyright text-center">
			<p>
				© <span>Copyright</span> <strong class="sitename px-1">Arkar Phyo</strong>
				<span>All Rights Reserved</span>
			</p>
		</div>
	</div>
</footer>

<!-- Scroll Top -->
<a href="#" id="scroll-top" class="scroll-top d-flex align-items-center justify-content-center"
	><i class="bi bi-arrow-up-short"></i></a
>

<!-- Preloader -->
<!-- <div id="preloader"></div> -->
<style>
	.progress-bar {
		height: 100%;
		background-color: #3498db; /* Replace with your color */
		transition: width 1.5s ease-in-out;
	}
</style>
