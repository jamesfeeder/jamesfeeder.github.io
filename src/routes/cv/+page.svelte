<script>
	import Anchor from '$lib/Anchor.svelte';
	import { PaperPlaneTilt } from 'phosphor-svelte';

	const skills = [
		'HTML',
		'CSS',
		'SCSS',
		'Tailwind CSS',
		'Mantine',
		'TypeScript',
		'JavaScript',
		'Dart',
		'Python',
		'C#',
		'React',
		'Svelte',
		'Flutter',
		'Unity',
		'Firebase',
		'Git'
	];

	/*
    {
			title: '',
      projectName: '',
			client: '',
      remark: '',
			time: '',
			description: '',
			works: [],
			techs: []
	  }
  */

	const workExp = [
		{
			title: 'Software Developer',
			client: "Banno's Diary",
			time: '2020 - Present',
			description: "Develop and Maintain Banno's Diary Line Sticker in-house tools and website.",
			works: [
				"<a href='https://sticker.bannodiary.com' target='_blank' class='text-blue-600 hover:underline'>Banno's Diary Web Application</a>",
				"Banno's Diary Web Content Management System",
				"Banno's Diary Sticker Renderer"
			],
			techs: [
				'Python',
				'PIL',
				'OpenCV',
				'TkInter',
				'React',
				'Firebase Cloud Firestore',
				'Firebase Storage',
				'Google Docs API'
			]
		},
		{
			title: 'Web Developer',
			projectName: 'Agri Way',
			client: 'Yala Warehouse (1442) Ltd.',
			time: '2024',
			description: 'Web application for manage and track agricultural products.',
			techs: [
				'React',
				'Mantine',
				'Firebase Authentication',
				'Firebase Cloud Functions',
				'Firebase Cloud Firestore',
				'Firebase Storage'
			]
		},
		{
			title: 'Web Developer',
			projectName: 'GSB Wisdom Gamification',
			client: 'M & SULLIVAN',
			time: '2024',
			description:
				'Quiz game for GSB Wisdom LMS for train employee.',
			works: [
				"<a href='https://gsb-wisdom-identity.pages.dev' target='_blank' class='text-blue-600 hover:underline'>GSB Wisdom: Identification Quiz</a>",
				"<a href='https://gsb-wisdom-signature.pages.dev' target='_blank' class='text-blue-600 hover:underline'>GSB Wisdom: Signature Quiz</a>",
			],
			techs: ['React', 'React Spring', 'Howler.js', 'SCORM']
		},
		{
			title: 'Web Developer',
			projectName: 'SP HR SYSTEM',
			client: 'Southern Plastic',
			time: '2023',
			description: 'Develop web application for calculate man-hours and wages from timestamp data.',
			techs: [
				'React',
				'Mantine',
				'Firebase Authentication',
				'Firebase Cloud Functions',
				'Firebase Cloud Firestore',
				'Firebase Storage'
			]
		},
		{
			title: 'Game Developer',
			projectName: 'Real Me Hematologist',
			client: 'ShipHouse Production',
			time: '2023',
			description:
				'Develop online multi-player serious game for Faculty of Medicine, Prince of Songkla University.',
			works: [
				'Game Designer',
				'Game Programmer',
				'UX/UI Designer (Playable Prototype Version)',
				'UI Animator'
			],
			techs: ['Unity', 'C#', 'Photon PUN']
		},
		{
			title: 'Game Developer',
			projectName: 'Waste Town (Academic Project)',
			client: 'PSUIC',
			time: '2022',
			description:
				'2D Game for raising social responsibility about waste management reference environment in Thailand. Collaborate with Prakakit Ananlertsakul',
			works: ['Game Designer', 'Game Level Designer', 'Game Programmer', 'UI Animator'],
			techs: ['Unity', 'C#', 'URP', 'Light2D', 'Shader Graph']
		},
		{
			title: 'Web Developer',
			projectName: 'CMDT Website',
			client: 'PSUIC',
			time: '2021',
			description: 'Develop custom WordPress child theme. for PSUIC CMDT Program Website',
			techs: ['SCSS', 'WordPress', 'PHP']
		},
		{
			title: 'Mobile Application Developer',
			projectName: 'SABISU',
			client: 'National Software Contest',
			remark: '2<sup>nd</sup> Runner Up',
			time: '2020',
			description: 'SABISU, applications for businesses and SMEs Project Manageger',
			techs: ['Flutter', 'Firebase']
		},
		{
			title: 'Web Developer',
			projectName: 'FSC Tracking',
			client: 'IQC THAILAND',
			time: '2020',
			description: 'Develop and database design for website for manage customer data.',
			techs: ['Flutter Web', 'Firebase']
		},
		{
			title: 'Web Developer',
			projectName: 'Covid-19 Tracking Status',
			client: 'PSUIC',
			time: '2020 - 2021',
			description: 'Develop Covid-19 statistic website focus in Songkhla and University area.',
			techs: ['Flutter Web', 'Firebase']
		},
		{
			title: 'Mobile Application Developer',
			projectName: 'My Caregiver',
			client: 'National Software Contest',
			tags: ['Finalist'],
			time: '2019',
			description: 'My Caregiver, applications for patients and caregivers',
			techs: ['Ionic Frameworks 3', 'Firebase']
		}
	];

	const eduExp = [
		{
			program: 'International College, Digital Media',
			school: 'Prince of Songkla University, Hatyai Campus',
			time: '2018-2022'
		},
		{
			program: 'Sci-Math Ability Program',
			school: 'Hatyaiwittayalai School, Songkhla',
			time: '2012-2017'
		}
	];
</script>

<svelte:head>
	<title>jamesfeeder's cv</title>
</svelte:head>

<main class="mx-auto max-w-4xl p-4 pt-20 sm:p-6 sm:pt-20">
	<header class="flex flex-col justify-between gap-4 sm:flex-row">
		<div>
			<h1 class="text-3xl font-semibold text-slate-800">Jetsadakorn Maliwan</h1>
			<div class="flex flex-wrap items-center gap-1.5 pt-4">
				<p class="font-light text-slate-500">Software Developer /</p>
				<p class="font-light text-slate-500">Front-End Web Developer</p>
			</div>
		</div>
		<div class="flex flex-col items-start sm:items-end">
			<Anchor label="jetsadakorn.maliwan@gmail.com" link="mailto:jetsadakorn.maliwan@gmail.com"
				><PaperPlaneTilt weight="bold" /></Anchor
			>
			<Anchor label="github.com/jamesfeeder" link="https://github.com/jamesfeeder" openNewTab />
		</div>
	</header>

	<section id="skills" class="flex flex-wrap gap-2 pt-6 sm:w-3/4">
		{#each skills as skill}
			<p class="rounded-3xl bg-blue-600 px-3 py-1 text-sm font-semibold text-white">{skill}</p>
		{/each}
	</section>

	<section id="exp" class="pt-4">
		<h2 class="py-4 text-2xl font-semibold text-slate-800">Experience</h2>
		{#each workExp as exp, index}
			<h3 class="text-xl text-slate-600">{@html exp.title}</h3>
			{#if exp.projectName}
				<p class="text-base text-slate-600">Project: {exp.projectName}</p>
			{/if}
			<div class="flex items-center gap-2 py-1">
				<p class="text-lg font-semibold text-slate-800">{@html exp.client}</p>
				<p
					class="flex-none rounded-3xl bg-blue-600 px-2 py-1 text-center text-xs font-semibold text-white"
				>
					{exp.time}
				</p>
				{#if exp.remark}
					<p
						class="line-clamp-1 flex-none rounded-3xl bg-blue-600 px-2 py-1 text-center text-xs font-semibold text-white"
					>
						{@html exp.remark}
					</p>
				{/if}
			</div>
			<p class="p1-1 pb-2">{@html exp.description}</p>
			{#if exp.works}
				<div class="mb-2">
					<p class="flex items-center gap-1 pb-1 font-semibold">Works / Position</p>
					<ul role="list" class="list-inside list-disc">
						{#each exp.works as work}
							<li>{@html work}</li>
						{/each}
					</ul>
				</div>
			{/if}
			{#if exp.techs}
				<div class="flex flex-wrap gap-2 pb-2">
					{#each exp.techs as tech}
						<p
							class="rounded-3xl border border-blue-200 bg-blue-100 px-2 py-1 text-xs font-semibold text-slate-600"
						>
							{tech}
						</p>
					{/each}
				</div>
			{/if}
			{#if workExp.length - 1 > index}
				<div class="h-4" />
			{/if}
		{/each}
	</section>

	<section id="edu" class="pt-4">
		<h2 class="py-4 text-2xl font-semibold text-slate-800">Education</h2>
		{#each eduExp as exp, index}
			<div class="flex items-center gap-2">
				<p class="text-xl text-slate-600">{@html exp.program}</p>
				<p
					class=" flex-none rounded-3xl bg-blue-600 px-2 py-1 text-center text-xs font-semibold text-white"
				>
					{exp.time}
				</p>
			</div>
			<h3 class="pt-1 text-lg font-semibold text-slate-800">{@html exp.school}</h3>
			{#if eduExp.length - 1 > index}
				<div class="h-4" />
			{/if}
		{/each}
	</section>
</main>
