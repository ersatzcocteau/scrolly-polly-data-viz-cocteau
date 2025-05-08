<script lang="ts">
	// ===================================================================
	// MAIN APPLICATION COMPONENT
	// Configures and integrates scrollyteller with visualizations
	// ===================================================================
	import Scrollyteller, { loadScrollyteller } from '$lib/index.js';
	import VegaChart from './VegaChart.svelte';
	import { onMount } from 'svelte';

	// Import chart specifications from JSON files
	import chart01 from './Charts/chart_01.json';
	import chart03 from './Charts/chart_03.json';
	import chart04 from './Charts/chart_04.json';
	import chart06 from './Charts/chart_06.json';
	import chart07 from './Charts/chart_07.json';
	
	// ===================================================================
	// SCROLLYTELLER CONFIGURATION
	// Initialize scrollyteller with configuration parameters
	// ===================================================================
	const scrollyData = loadScrollyteller(
		'test', // Scrollyteller name - corresponds to #scrollytellerNAMEtest in CoreMedia
		'u-full', // Class for mount point - u-full makes it full width in Odyssey
		'mark' // Marker prefix - #markNUMBER1 etc. in CoreMedia
	);

	// App state
	let number = 0; // Current section number
	let stProgress; // Scrollyteller progress data
	let currentSpec = null; // Current chart specification

	// ===================================================================
	// CHART METADATA
	// Content information for each visualization section
	// ===================================================================
	const chartInfo = [
		{
			title: "The Beginning",
			description: "The foundation of our future is being built today, with technologies that will reshape how we live, work, and interact with the world around us.",
			alignment: "left"
		},
		{
			title: "Digital Transformation",
			description: "As digital technologies become increasingly integrated into every aspect of our lives, the boundary between physical and virtual continues to blur.",
			alignment: "center"
		},
		{
			title: "Global Connectivity",
			description: "The world becomes more interconnected each day, creating new opportunities for collaboration and innovation across traditional boundaries.",
			alignment: "right"
		},
		{
			title: "Artificial Intelligence",
			description: "AI systems are evolving from simple automation tools to creative partners, augmenting human capabilities and reshaping how we solve complex problems.",
			alignment: "left"
		},
		{
			title: "Sustainable Technology",
			description: "The pressing need for environmental solutions is driving innovation toward technologies that can help us create a more sustainable future for our planet.",
			alignment: "center"
		},
		{
			title: "New Frontiers",
			description: "From space exploration to quantum computing, emerging technologies are opening up entirely new possibilities that were once confined to science fiction.",
			alignment: "right"
		},
		{
			title: "Human-Technology Convergence",
			description: "The integration of technology with human biology and cognition represents perhaps the most profound transformation in our evolutionary journey.",
			alignment: "center"
		}
	];

	// ===================================================================
	// EVENT HANDLERS
	// Handle scrollyteller events for markers and progress
	// ===================================================================
	
	// Handle marker changes (when user scrolls to a new section)
	const onMarker = (marker) => {
		number = marker.number;
		updateVisualization(number);
	};

	// Track scrolling progress for animations
	const onProgress = (progress) => {
		stProgress = progress;
	};

	// ===================================================================
	// VISUALIZATION MANAGEMENT
	// Update displayed content based on current section
	// ===================================================================
	
	// Update the visualization based on the current marker number
	function updateVisualization(markerNumber) {
		// Select the appropriate chart specification for each section
		switch (markerNumber) {
			case 1:
				currentSpec = chart01; // Chart visualization
				break;
			case 2:
				currentSpec = null; // Full-screen image instead of chart
				break;
			case 3:
				currentSpec = chart03; // Chart visualization
				break;
			case 4:
				currentSpec = chart04; // Chart visualization
				break;
			case 5:
				currentSpec = null; // Full-screen image instead of chart
				break;
			case 6:
				currentSpec = chart06; // Chart visualization
				break;
			case 7:
				currentSpec = chart07; // Chart visualization
				break;
			default:
				currentSpec = null;
				break;
		}
	}

	// Initialize with first visualization on component mount
	onMount(() => {
		updateVisualization(1);
	});
</script>

<svelte:head>
	<!-- 
	// ===================================================================
	// FONT IMPORTS
	// Typography resources for the application
	// ===================================================================
	-->
	<link rel="preconnect" href="https://fonts.googleapis.com">
	<link rel="preconnect" href="https://fonts.gstatic.com">
	<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300..700;1,300..700&family=Figtree:ital,wght@0,300..900;1,300..900&family=Fleur+De+Leah&family=IBM+Plex+Mono:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;1,100;1,200;1,300;1,400;1,500;1,600;1,700&family=Instrument+Serif:ital@0;1&family=Roboto+Condensed:ital,wght@0,100..900;1,100..900&display=swap" rel="stylesheet">
	<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300..700;1,300..700&family=Figtree:ital,wght@0,300..900;1,300..900&family=Fira+Sans:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&family=Fleur+De+Leah&family=IBM+Plex+Mono:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;1,100;1,200;1,300;1,400;1,500;1,600;1,700&family=Instrument+Serif:ital@0;1&family=Roboto+Condensed:ital,wght@0,100..900;1,100..900&family=Space+Mono:ital,wght@0,400;0,700;1,400;1,700&display=swap" rel="stylesheet">
</svelte:head>

<!-- 
// ===================================================================
// HEADER SECTION
// Full-screen hero image with title overlay
// ===================================================================
-->
<div class="fullscreen-chapter header-image">
	<div class="header-overlay"></div>
	<div class="header-content">
		<h1 class="main-title">Timeline to the Future</h1>
		<h2 class="sub-title">Martina and Rosario // May 2025</h2>
	</div>
</div>

<!-- 
// ===================================================================
// INTRODUCTION CONTENT
// Opening paragraphs before scrollytelling sections
// ===================================================================
-->
<div class="content-container">
	<p class="content-paragraph">The future unfolds before us, shaped by technological innovations that transform how we live, work, and connect. This exploration charts the course of these developments, from early breakthroughs to the revolutionary changes on the horizon. Through data visualization and narrative, we examine the forces driving us toward tomorrow.</p>
	<p class="content-paragraph">We stand at a unique moment in human history, where the pace of change continues to accelerate. Technologies that seemed like science fiction a decade ago are now becoming commonplace, while new possibilities emerge daily. Understanding these dynamics helps us navigate the opportunities and challenges ahead.</p>
	<div class="image-left">
		<img src="../../src/TestExample/Images/placeholder.png" alt="Technology concept" />
	</div>
	<p class="content-paragraph">This journey through our technological future examines both the tangible innovations being developed today and their potential long-term impacts. We'll explore how emerging technologies intersect and amplify each other, creating new possibilities that transform industries, communities, and individual lives.</p>
	<p class="content-paragraph">Beyond the technical details, we'll consider how these changes affect human experience and social structures. The most profound impacts often come not from the technologies themselves, but from how they reshape our relationships, institutions, and understanding of ourselves.</p>
</div>

<!-- 
// ===================================================================
// CHAPTER SECTION - BLACK
// Full-screen black background section with white text
// ===================================================================
-->
<div class="fullscreen-chapter black-bg">
	<div class="content-container">
		<h2>Navigating Change</h2>
		<p class="content-paragraph">The evolution of technology rarely follows a linear path. Instead, it emerges through complex interactions between scientific breakthroughs, social needs, economic incentives, and cultural values. By mapping these relationships, we can better anticipate how current developments might evolve into transformative solutions.</p>
		<p class="content-paragraph">Throughout history, technological shifts have been accompanied by social and institutional adaptations. As we develop increasingly powerful tools, we simultaneously need to evolve our frameworks for governance, ethics, and meaning-making. The most successful transitions occur when technological and social innovation advance in harmony.</p>
		<p class="content-paragraph">The visualizations that follow represent different dimensions of our technological future. Each offers a perspective on how specific innovations are evolving and converging to create new possibilities. Together, they illustrate the multifaceted nature of technological change and its implications for humanity's path forward.</p>
	</div>
</div>

<!-- 
// ===================================================================
// MAP VISUALIZATION
// Embedded Datawrapper map visualization
// ===================================================================
-->
<div style="min-height:730px" id="datawrapper-vis-V8sUH"><script type="text/javascript" defer src="https://datawrapper.dwcdn.net/V8sUH/embed.js" charset="utf-8" data-target="#datawrapper-vis-V8sUH"></script><noscript><img src="https://datawrapper.dwcdn.net/V8sUH/full.png" alt="" /></noscript></div>

<div class="content-container">
	<p class="content-paragraph">Innovation ecosystems are emerging globally as technology development becomes increasingly distributed. While traditional centers like Silicon Valley remain important, new hubs are arising across Asia, Europe, Africa, and Latin America, each with distinctive strengths and approaches. This geographical diversification accelerates cross-pollination of ideas.</p>
	<p class="content-paragraph">Different regions emphasize diverse technological priorities based on their specific challenges, resources, and cultural values. These variations create a natural laboratory where multiple approaches can be tested simultaneously. The most successful innovations often incorporate insights from these diverse perspectives.</p>
	<div style="min-height:430px" id="datawrapper-vis-FkN5a"><script type="text/javascript" defer src="https://datawrapper.dwcdn.net/FkN5a/embed.js" charset="utf-8" data-target="#datawrapper-vis-FkN5a"></script><noscript><img src="https://datawrapper.dwcdn.net/FkN5a/full.png" alt="" /></noscript></div>
	<p></p>
	<p class="content-paragraph">Investment patterns reveal shifting priorities in technological development. Funding increasingly flows toward innovations that address critical challenges in sustainability, healthcare access, and digital inclusion. This reallocation of resources accelerates progress in these domains while potentially slowing development in others.</p>
	<p class="content-paragraph">The timeline to widespread adoption varies significantly across technologies. Some innovations, particularly in software and digital services, can scale globally in months. Others, especially those requiring physical infrastructure or regulatory approval, may take decades to reach their full potential. Understanding these different timescales helps set realistic expectations for change.</p>
</div>

<!-- 
// ===================================================================
// SCROLLYTELLER COMPONENT
// Main scrollytelling section with data visualizations
// ===================================================================
-->
<Scrollyteller
	panels={scrollyData.panels}
	{onMarker}
	{onProgress}
>
	<div class="graphic">
		<div class="chart-container">
			<!-- Render different content based on current section -->
			{#if number === 1}
				<!-- Section 1: Chart with left alignment -->
				<VegaChart 
					spec={chart01}
					alignment={chartInfo[0].alignment} 
				/>
				
				<div class="chart-info align-left">
					<h3 class="chart-title">{chartInfo[0].title}</h3>
					<p class="chart-description">{chartInfo[0].description}</p>
				</div>
			
			{:else if number === 2}
				<!-- Section 2: Full-screen image -->
				<div class="fullscreen-image-container">
					<img src="../src/TestExample/Images/placehold-19201080-orange.png" alt="Digital transformation visualization" class="fullscreen-image" />
				</div>
			
			{:else if number === 3}
				<!-- Section 3: Chart with right alignment -->
				<VegaChart 
					spec={chart03}
					alignment={chartInfo[2].alignment} 
				/>
				
				<div class="chart-info align-right">
					<h3 class="chart-title">{chartInfo[2].title}</h3>
					<p class="chart-description">{chartInfo[2].description}</p>
				</div>
			
			{:else if number === 4}
				<!-- Section 4: Chart with left alignment -->
				<VegaChart 
					spec={chart04}
					alignment={chartInfo[3].alignment} 
				/>
				
				<div class="chart-info align-left">
					<h3 class="chart-title">{chartInfo[3].title}</h3>
					<p class="chart-description">{chartInfo[3].description}</p>
				</div>
			
			{:else if number === 5}
				<!-- Section 5: Full-screen image -->
				<div class="fullscreen-image-container">
					<img src="../src/TestExample/Images/placehold-19201080-blue.png" alt="Sustainability visualization" class="fullscreen-image" />
				</div>
			
			{:else if number === 6}
				<!-- Section 6: Chart with right alignment -->
				<VegaChart 
					spec={chart06}
					alignment={chartInfo[5].alignment} 
				/>
				
				<div class="chart-info align-right">
					<h3 class="chart-title">{chartInfo[5].title}</h3>
					<p class="chart-description">{chartInfo[5].description}</p>
				</div>
			
			{:else if number === 7}
				<!-- Section 7: Chart with center alignment -->
				<VegaChart 
					spec={chart07}
					alignment={chartInfo[6].alignment} 
				/>
				
				<div class="chart-info align-center">
					<h3 class="chart-title">{chartInfo[6].title}</h3>
					<p class="chart-description">{chartInfo[6].description}</p>
				</div>
			
			{:else}
				<!-- Default/Initial state before scrolling begins -->
				<div class="initial-state">
					<p>Scroll to begin the journey</p>
				</div>
			{/if}
		</div>
	</div>
</Scrollyteller>

<!-- 
// ===================================================================
// CONTENT SECTION
// Additional content after scrollytelling experience
// ===================================================================
-->
<div class="content-container">
	<p class="content-paragraph">The convergence of these technological streams will reshape what it means to be human in the coming decades. Boundaries between physical and digital realms will continue to blur, creating hybrid experiences that combine the best of both worlds. Our relationship with machines will become more symbiotic as AI systems become more capable of understanding context and collaborating effectively.</p>
	<p class="content-paragraph">As these tools become more powerful, questions of access and governance become increasingly important. Who benefits from these technologies, and who decides how they're developed and deployed? Creating inclusive approaches to innovation ensures that technological progress translates into broadly shared prosperity and wellbeing.</p>
	<p class="content-paragraph">The democratization of powerful technologies creates both opportunities and risks. As tools that were once restricted to specialized institutions become accessible to small teams and individuals, innovation can accelerate and diversify. However, this same dynamic makes governance more challenging, requiring new approaches to managing technologies with significant societal implications.</p>
	<p class="content-paragraph">Despite these challenges, there is reason for optimism. Human ingenuity has consistently found ways to channel technological change toward positive outcomes. By maintaining focus on core values like human dignity, environmental stewardship, and inclusive prosperity, we can shape these powerful tools to create a future that expands rather than diminishes human flourishing.</p>
</div>

<!-- 
// ===================================================================
// BEIGE CHAPTER SECTION
// Full-screen beige background section with contrast text
// ===================================================================
-->
<div class="fullscreen-chapter beige-bg">
	<div class="content-container">
		<h2>Shaping Our Future</h2>
		<p class="content-paragraph">The future isn't predetermined; it's created through countless decisions made by individuals, organizations, and societies. By understanding the technologies that will shape tomorrow, we can make more informed choices today. Each of us has a role in steering these powerful tools toward outcomes that align with our deepest values.</p>
		<p class="content-paragraph">Engagement is crucial. The future belongs to those who participate in creating it. Whether through technological development, policy advocacy, artistic expression, or ethical discourse, each contribution helps guide our collective journey toward a future we want to inhabit.</p>
	</div>
</div>

<div class="content-container">
	<p class="content-paragraph">Innovation increasingly happens at the intersection of disciplines. The most transformative developments often emerge when expertise from different domains combines in novel ways. This cross-pollination of ideas accelerates breakthrough solutions to complex challenges.</p>
	<p class="content-paragraph">Distributed collaboration enables global problem-solving at unprecedented scales. Digital platforms allow diverse participants to contribute regardless of location, creating powerful collective intelligence. These networked approaches are particularly effective for addressing multifaceted global challenges.</p>
	<div style="min-height:591px" id="datawrapper-vis-bbmLi"><script type="text/javascript" defer src="https://datawrapper.dwcdn.net/bbmLi/embed.js" charset="utf-8" data-target="#datawrapper-vis-bbmLi"></script><noscript><img src="https://datawrapper.dwcdn.net/bbmLi/full.png" alt="" /></noscript></div>	<p></p>
	<p class="content-paragraph">Long-term thinking becomes increasingly valuable in a world of accelerating change. By considering multiple time horizons simultaneously, we can better navigate immediate challenges while steering toward desirable futures. This balanced perspective helps avoid short-term solutions that create larger problems down the road.</p>
	<p class="content-paragraph">The most profound innovations often transform not just what we can do, but how we understand ourselves and our world. As we develop increasingly sophisticated tools, we simultaneously evolve new frameworks for making sense of our changing reality. This co-evolution of technology and meaning will define the coming decades.</p>
</div>

<!-- 
// ===================================================================
// FOOTER SECTION
// Site footer with contact links and additional information
// ===================================================================
-->
<footer class="site-footer">
	<div class="footer-container">
		<div class="footer-content">
			<h3 class="footer-heading">Timeline to the Future</h3>
			<p class="footer-text">A visual exploration of technological evolution and its impact on society.</p>
			<p class="footer-text">Created by Martina and Rosario, May 2025</p>
			<p class="footer-text">Contact: future@timelineproject.org</p>
		</div>
		<div class="footer-links">
			<p class="footer-text">This project is an adaptation of the <a href="https://github.com/abcnews/scrollyteller">Scrollyteller</a> by ABC News.</p>
		</div>
	</div>
</footer>