---
layout: page
title: "Ataxia and Clinical Genomics (ATCG) Lab"
banner: "../assets/img/banner/slider-bg-pale.jpg"
---
<meta name="twitter:card" content="summary" />
<meta name="twitter:site" content="@ATCG_Official" />
<meta name="twitter:creator" content="@ATCG_Official" />
<meta property="og:url" content="https://atcglab.github.io" />
<meta property="og:title" content="Ataxia and Clinical Genomics Lab" />
<meta property="og:description" content="Official lab website, live updates on current interests" />
<meta property="og:image" content="../assets/img/logo_covid.png"/>
<link rel="stylesheet" href="https://www.w3schools.com/w3css/4/w3.css">

<div class="content-new-info">
<br>
    <a href="https://atcglab.github.io/COVID-19.html" target="_blank"><img src="{{ site.baseurl }}/assets/img/logo_covid.png" alt="Course logo"></a>
    <div class="count">
<ul class="count-list">
	<li>
		<div>
            <i class="fas fa-line-chart"></i>
			<span class="counter">104</span>
			<span class="counter-desc">IGIB-NCDC</span>
		</div>
    </li>
    <li>
		<div>
            <i class="fas fa-flag"></i>
			<span class="counter">376</span>
			<span class="counter-desc">India</span>
		</div>
    </li>
    <li>
		<div>
            <i class="fas fa-globe"></i>
			<span class="counter">31852</span>
			<span class="counter-desc">World</span>
		</div>
	</li>
  </ul>
</div>
<big>The COVID-19 initiative from <a href="https://igib.res.in"><b>CSIR-Institute of Genomics and Integrative Biology (CSIR-IGIB)</b></a> in collaboration with <a href="https://ncdc.gov.in/"><b>National Centre for Disease Control (NCDC)</b></a> has been serving for national interest during this pandemic by sequencing and understanding the biology of COVID genome. Through this program, CSIR-IGIB is joining hands for the sequencing of SARS-CoV-19 genome all over India. Live updates on the COVID-19 research in India and lab's interests will be updated <a href="https://atcglab.github.io/COVID-19.html">here</a>.</big>
</div>
<section id="index-work" style="padding-bottom:20px">
<div class="container">
        <center><a class="button-newest" href="https://nextstrain.org/community/bharathramh/ATCG/ncov" target="_blank">COVID-19 Initiative</a>         <a class="button-new" href="{{ site.baseurl }}/COVID-19">Learn more about this</a>         <a class="button" href="{{ site.baseurl }}/involve">Collaborate with us</a></center>
  </div>
</section>

<section id="portfolio-work" style="background-color: #c4d7d7; padding-bottom:20px; padding-top:20px">
<div class="content-new-streams">
    <img src="{{ site.baseurl }}/assets/img/about.jpg" style= "width:25%; height:auto; padding:20px;20px;20px;80px;" alt="About us"><h1>About us</h1>

<p>Welcome!</p>

<p>We are situated in the heart of one of the most premier government institutes by the Council of Scientific and Industrial Research (CSIR), Institute of Genomics and Integrative Biology (IGIB). Our Functional Genomics Laboratory works closely towards bridging the gap between the fundamentals of Genomics and its translational approaches to better comprehend the dictated mechanisms leading to human diseases specifically, neurodegenerative ailments for their prognosis and prevention. Time and again, we have been a part of government initiatives and projects to understand diseases at an individual and population level better, like the <a href="http://www.igvdb.res.in"><b>Indian Genome Variation Project (IGV)</b></a>, under which 1800 individuals from 55 ethnic groups were studied at the Single Nucleotide Polymorphism (SNP) level and the project was completed within two years of its announcement. Subsequently, we became the chief laboratory to provide free equitable access to genetic testing for frequent genetic diseases to underprivileged patients countrywide through Government-funded program, the <a href="http://gomed.igib.in"><b>Genomics and other Omics technologies for Enabling Medical Decision (GOMED)</b></a> comprising of genetic investigation of greater than 60 conditions from <b>Spinocerebellar Ataxia</b> to Molecular Dystrophy where we have genetically addressed about 10,000 patient samples till now. Apart from this, ever since its inception, our laboratory has been committed to research in genetically and clinically heterogeneous group of rare neurodegenerative disorders, Spinocerebellar Ataxias (SCAs) as a large variety of genetic mutations are associated with them comprising of dynamic Tandem Nucleotide Repeat (TNR) expansion, Point mutation, Insertion and Deletion. With varying genetic profiles, specific experimentations and validations are carried out, for instance, Autosomal Dominant SCAs (ADCAs), caused more often by repeat expansions are validated by Fluorescent labelled primer-based PCR reaction or Triplet Primed (TP) PCR followed by Fragment Analysis method, whereas, Autosomal Recessive SCAs (ARCAs) caused due to repeat expansion (FRDA) or point mutation are confirmed using TP-PCR followed by Fragment Analysis or Sanger Sequencing method. We also refer to Next-Generation Sequencing (NGS) technologies, especially Exome sequencing to usually solve genetically negative samples. The other major part of our research also focuses on genotype to phenotype correlation, where we study the pathogenesis of various neurodegenerative disorders like Spinocerebellar Ataxias (SCAs), FRDA along with finding their therapeutic targets. Since, it is quite challenging to get post-mortem autopsy tissues of the brain of the patient suffering from neurological disorders in India, we therefore, generate Lymphoblastoid Cell Lines (LCLs) from Peripheral Blood Mononuclear Cells (PBMCs) of patients in our lab. Subsequently, to study the specific brain pathologies in these diseases, we also develop Induced Pluripotent Stem Cells (iPSCs) from LCLs and further differentiate these iPSCs to Neurons, to recapitulate the environment existing in the patient nerve cells. Thus, as an ideal model, it helps us in studying specific molecular perturbations at large. Currently, we have more than 40 cellular models of different patients and our future goal is to include even more diseases in our stem cell repository to elucidate their pathogenesis for therapeutic interventions as our ultimate vision is healthcare.</p>
</div>
</section>


{%- capture twitter -%}
https://twitter.com/{{ author.twitter }}
{%- endcapture -%}

{% include link-button.html url=twitter button="Follow us on Twitter and find out about our latest updates!" target="_blank" %}


<div class="w3-content w3-section">
	<img class="mySlides" src="{{ site.baseurl }}/assets/img/index/workshop1.JPG" alt="Workshop photo">
	<img class="mySlides" src="{{ site.baseurl }}/assets/img/index/workshop2.JPG" alt="Workshop photo">
	<img class="mySlides" src="{{ site.baseurl }}/assets/img/index/workshop4.JPG" alt="Workshop photo">
	<img class="mySlides" src="{{ site.baseurl }}/assets/img/index/workshop5.JPG" alt="Workshop photo">
</div>

<script>
var myIndex = 0;
carousel();

function carousel() {
  var i;
  var x = document.getElementsByClassName("mySlides");
  for (i = 0; i < x.length; i++) {
    x[i].style.display = "none";  
  }
  myIndex++;
  if (myIndex > x.length) {myIndex = 1}    
  x[myIndex-1].style.display = "block";  
  setTimeout(carousel, 2000); // Change image every 2 seconds
}
</script>



<section id="portfolio-work" style="padding-top:10px">
<div class="content-new-info">
<center><h2>Our values and goals</h2></center>
<div class="values">
<ul>
	<li>
		<div>
            <i class="fas fa-image"></i>
			<span class="values-title">Quantitative skills</span>
			<span class="values-desc">We empower students and future professionals to answer research questions and harness the power of data</span>
		</div>
    </li>
    <li>
		<div>
            <i class="fas fa-leaf"></i>
			<span class="values-title">Sustainable learning</span>
			<span class="values-desc">We support the future development of Coding Club through mentorship and training</span>
		</div>
    </li>
    <li>
		<div>
            <i class="fas fa-globe-europe"></i>
			<span class="values-title">Collaboration in learning</span>
			<span class="values-desc">We establish links between organisations and institutions which develop quantitative skills</span>
		</div>
	</li>
    <li>
      <div>
            <i class="fas fa-handshake"></i>
			<span class="values-title">Diversity</span>
			<span class="values-desc">Fostering a supportive and inclusive environment with diverse opportunities to learn</span>
      </div>
    </li>
  </ul>
</div>
</div>
</section>



<a name = "coursebrief"></a>
<section id="portfolio-work" style="background-color: #a6d4dc; padding-bottom:20px">
<div class="content-new-info">
<a href="https://ourcodingclub.github.io/course" target="_blank"><img src="{{ site.baseurl }}/assets/img/dl_course/course-details-tall.png" style= "width:30%; height:auto; padding:20px;20px;20px;80px;" alt="Data Science course details"></a>
<h2><b>Data Science for Ecologists and Environmental Scientists</b> - a free online course</h2>
<p><b><a href="https://ourcodingclub.github.io/course" target="_blank">Data Science for Ecologists and Environmental Scientists</a> is an online learning initiative for anyone wanting to gain data science skills in the programming language R, with additional content in Python and JavaScript. Our motivation is to overcome "code fear" and "statistics anxiety" in learners of all ages and from all walks of life. This course is developed for international audiences, but is also uniquely Scottish with real-world data to put quantitative skills into the context of key ecological questions.</b></p>

<p>The three course themes introduce learners to key elements of data science - ‘<a href="https://ourcodingclub.github.io/course/stats-scratch/index.html" target="_blank">Stats from Scratch</a>’, ‘<a href="https://ourcodingclub.github.io/course/wiz-viz/index.html" target="_blank">Wiz of Data Vis</a>’ and ‘<a href="https://ourcodingclub.github.io/course/mastering-modelling/index.html" target="_blank">Mastering Modelling</a>’. The 16 individual tutorials that make up the course, in addition to the further 25 tutorials hosted by <a href="https://ourcodingclub.github.io/tutorials.html" target="_blank">Coding Club</a>, allow learners to create their own bespoke learning pathway to gaining key skill sets. Quizzes and challenges test knowledge, but also allow users to join a larger community of learners and gain confidence in their own skills. Join the hundreds of thousands of Coding Club users and develop your data science skills through this entirely free and engaging online learning initiative!</p>
<br>
<section id="index-work" style="padding-bottom:20px">
<div class="container">
<a class="button-new" href="{{ site.baseurl }}/course">Learn more about the course</a>
</div>
</section>
</div>
</section>
<br>
<section id="portfolio-work" style="background-color: #f4eddc; padding-bottom:20px">
<div class="content-new-streams">
<a href="https://datascienceees.github.io" target="_blank"><img src="{{ site.baseurl }}/assets/img/index/ds-edi.png" style= "width:20%; height:auto; padding:20px;20px;20px;80px;" alt="Data Science in Edinburgh logo"></a>
<h2>Data Science in Edinburgh</h2>
<p><b><h4><a href="https://drive.google.com/file/d/16lpxNNEq8lnqWWB2S8kUoyYPyigAM0dk/view?usp=sharing" target="_blank">Schedule for Edinburgh workshops in 2020!</a></h4></b></p>

<p><big>Building on Coding Club, we have also started a new 4th year Data Science in Ecology and Environmental Science honours-level undergraduate course at the University of Edinburgh - you can find out course website and curriculum <a href="https://datascienceees.github.io" target="_blank">here</a>.</big></p>
</div>
</section>

<section id="portfolio-work" style="padding-bottom:1px">
<div class="content-new-info">
<h2>News</h2>
</div>
</section>
* 22nd February 2020 - [Coding Club is running a brand new free online data science course]({{ site.baseurl }}/course/) 
* 17th February 2020 - [A new advanced data viz and data synthesis tutorial from our workshop at the University of Glasgow]({{ site.baseurl }}/tutorials/dataviz-beautification-synthesis/) 
* 5th February 2020 - [A new tutorial - ultimate figure beautification from our workshop at the University of Boulder]({{ site.baseurl }}/tutorials/dataviz-beautification/) 
* 23rd January 2020 - [Google dataset search out of beta](https://blog.google/products/search/discovering-millions-datasets-web/)
* 22nd January 2020 - [Preview of rconf 2020](https://web.cvent.com/event/36ebe042-0113-44f1-8e36-b9bc5d0733bf/summary?RefId=conference)
* 19th January 2020 - [Rbloggers: Top 40 new R packages](https://www.r-bloggers.com/december-2019-top-40-new-r-packages/)
* 17th October 2018 - [Quantitative skills and Coding Club - a blog post for the Software Sustainability Institute](https://software.ac.uk/blog/2018-10-17-coding-club-peer-learning-programming-statistics-and-data-science)

<section id="portfolio-work">
<div class="content-new-info">
<h2>Contribute</h2>
<p><b>Our mission is to support a diverse learning community where we help each other to attain fluency in statistics and programming.</b> We are very keen to expand our team and anyone can join in! We are looking for people interested in <a href="https://ourcodingclub.github.io/involve.html" target="_blank">contributing tutorials and/or hosting workshops</a>. You can also check out <a href="https://dynamicecology.wordpress.com/2018/10/25/guest-post-coding-club-trying-to-overcome-the-fear-factor-in-teaching-and-learning-quantitative-skills/" target = "_blank">our blog post on Dynamic Ecology for more about our teaching philosophy</a>. Feel free to contact us with any questions or feedback: we would really appreciate your input!</p>
</div>
</section>

{%- capture link -%}
{{ site.baseurl }}/contact/
{%- endcapture -%}
{% include link-button.html url=link button="Get in touch" %}

<section id="portfolio-work">
<div class="content-new-info">
<h2>Funding</h2>

<p>Coding Club was jumpstarted with support from an <a href="http://www.ed.ac.uk/development-alumni/iig" target="_blank">Innovation Initiative Grant</a> from the Edinburgh Fund at the University of Edinburgh. We organised our first joint workshop with the University of Aberdeen with the help of a GESA Innovation Initiative Grant. We took Coding Club further with the help of a <a href="http://www.ed.ac.uk/institute-academic-development/learning-teaching/funding/funding/previous-projects/year/march-2017/coding-club" target="_blank">Principal's Teaching Award Scheme grant</a>. We are working together with the <a href="http://e3dtp.geos.ed.ac.uk/" target="_blank">NERC E3 Doctoral Training Partnership</a> which supports some of our team members. Our <a href="https://ourcodingclub.github.io/course" target="_blank">Data Science for Ecologists and Environmental Scientists course</a> is funded by <a href="https://www.thedatalab.com" target="_blank">the Data Lab</a> in Scotland.</p>

<img src="{{ site.baseurl }}/assets/img/index/data-lab-logo.png" style= "width: 30%; height:auto" alt="Data Lab logo"><img src="{{ site.baseurl }}/assets/img/index/UoE_InnovationGrants_logo_2COL300dpi.jpg" style= "width: 30%; height:auto" alt="Innovation Initiative Grant logo"><img src="{{ site.baseurl }}/assets/img/index/dtp_for_cc.jpg" style= "width: 30%; height:auto" alt="DTP and NERC logos">
</div>
</section>

{% include call.html %}
