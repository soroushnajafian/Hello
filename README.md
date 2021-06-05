
<!DOCTYPE html>
<html lang="en-us">

  <head>
  <link href="http://gmpg.org/xfn/11" rel="profile">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta http-equiv="content-type" content="text/html; charset=utf-8">

  <!-- Enable responsiveness on mobile devices-->
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1">
 <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script> 	
  <title>
    
      Bayesian Linear Regression using PyMC3  &middot; 
    
  </title>

  <!-- CSS -->
  <link rel="stylesheet" href=" /public/css/poole.css">
  <link rel="stylesheet" href=" /public/css/syntax.css">
   <link rel="stylesheet" href=" /public/css/syntax.css">
  <link rel="stylesheet" href=" /public/css/hyde.css">
  <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=PT+Sans:400,400italic,700|Abril+Fatface">
  <link rel="stylesheet" href=" /public/css/font-awesome/css/font-awesome.min.css">

  <!-- Icons -->
  <link rel="apple-touch-icon-precomposed" sizes="144x144" href="public/apple-touch-icon-144-precomposed.png">
                                 <link rel="shortcut icon" href="public/favicon.ico">

  <!-- RSS -->
  <link rel="alternate" type="application/rss+xml" title="RSS" href="/atom.xml">
  <!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=UA-137872731-1"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'UA-137872731-1');
</script>

  <!-- Begin Jekyll SEO tag v2.6.1 -->
<title>Bayesian Linear Regression using PyMC3 | Prasad Ostwal</title>
<meta name="generator" content="Jekyll v3.9.0" />
<meta property="og:title" content="Bayesian Linear Regression using PyMC3" />
<meta name="author" content="Prasad Ostwal" />
<meta property="og:locale" content="en_US" />
<meta name="description" content="Bayesian Linear Regression using PyMC3" />
<meta property="og:description" content="Bayesian Linear Regression using PyMC3" />
<link rel="canonical" href="http://ostwalprasad.github.io/machine-learning/Bayesian-Linear-Regression-using-PyMC3.html" />
<meta property="og:url" content="http://ostwalprasad.github.io/machine-learning/Bayesian-Linear-Regression-using-PyMC3.html" />
<meta property="og:site_name" content="Prasad Ostwal" />
<meta property="og:type" content="article" />
<meta property="article:published_time" content="2019-04-16T18:28:43+00:00" />
<script type="application/ld+json">
{"@type":"BlogPosting","headline":"Bayesian Linear Regression using PyMC3","dateModified":"2019-04-16T18:28:43+00:00","datePublished":"2019-04-16T18:28:43+00:00","mainEntityOfPage":{"@type":"WebPage","@id":"http://ostwalprasad.github.io/machine-learning/Bayesian-Linear-Regression-using-PyMC3.html"},"author":{"@type":"Person","name":"Prasad Ostwal"},"url":"http://ostwalprasad.github.io/machine-learning/Bayesian-Linear-Regression-using-PyMC3.html","description":"Bayesian Linear Regression using PyMC3","@context":"https://schema.org"}</script>
<!-- End Jekyll SEO tag -->

  
</head>



  <body >

    <div class="sidebar">
  <div class="container sidebar-sticky">
    <div class="sidebar-about">
      <h1>
        <a href="">
          Prasad Ostwal
        </a>
      </h1>
      <p class="lead">My personal blog of tech and life</p>
    </div>

    <nav class="sidebar-nav">
      <a class="sidebar-nav-item" href="">Home</a>

      

      
      
        
          
        
      
        
          
            <a class="sidebar-nav-item" href="/Blog/">Blog</a>
          
        
      
        
          
            <a class="sidebar-nav-item" href="/medium/">Medium</a>
          
        
      
        
          
            <a class="sidebar-nav-item" href="/about.html">About Me</a>
          
        
      
        
      
        
          
        
      
        
      
        
      
        
      
        
      
        
          
        
      
		

      
      <a href="https://github.com/ostwalprasad" target="_blank" style="text-decoration:none">
        <i class="fa fa-fw fa-github"></i>
      </a>
      
      
      
      <a href="https://linkedin.com/in/ostwalprasad" target="_blank" style="text-decoration:none">
        <i class="fa fa-fw fa-linkedin"></i>
      </a>
      
	  
      
      <a href="https://twitter.com/ostwalprasad" target="_blank" style="text-decoration:none">
        <i class="fa fa-fw fa-twitter"></i>
      </a>
      
	  
	  
      <a href="mailto:prasadostwal@gmail.com" target="_blank" style="text-decoration:none">
        <i class="fa fa-envelope-o" aria-hidden="true"></i>
      </a>
      
	  
	  
	  
	  
    
      <span class="sidebar-nav-item">Currently v1.0.3</span>
	  
    </nav>


    <p>&copy; 2020. All rights reserved.</p>
  </div>
</div>


    <div class="content container">
  <script type="text/x-mathjax-config">
    MathJax.Hub.Config({
      tex2jax: {
        skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
        inlineMath: [['$','$']]
      }
    });
  </script>
  <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script> 	
<article class="post h-entry" itemscope itemtype="http://schema.org/BlogPosting">

  <header class="post-header">
    <h1 class="post-title p-name" itemprop="headline">Bayesian Linear Regression using PyMC3 </h1>
	
    <p class="post-meta">
      <time class="dt-published" datetime="2019-04-16T18:28:43+00:00" itemprop="datePublished">Apr 16, 2019
      </time>• <span itemprop="author" itemscope itemtype="http://schema.org/Person"><span class="p-author h-card" itemprop="name">Prasad Ostwal</span></span>• machine-learning
	  </p>
  </header>
  

<hr size="4" width="100%" align="left" color="black">
  <div class="post-content e-content" itemprop="articleBody">
    <h3 id="introduction">Introduction</h3>

<blockquote>
  <p>In statistics, Bayesian linear regression is an approach to linear regression in which the statistical analysis is undertaken within the context of Bayesian inference. When the regression model has errors that have a normal distribution, and if a particular form of prior distribution is assumed, explicit results are available for the posterior probability distributions of the model’s parameters.</p>
</blockquote>

<p><strong>Linear Regression</strong></p>

<p>In simple linear regression we get point estimates by</p>

\[y = \alpha\ + \beta\ *x\]

<p>Equation says, there’s a linear relationship between variable $x$ and $y$. Slope is controlled by $ \beta\ $ and intercept tells about value of $y$ when $x=0$ . Methods like Ordinary Least Squares, optimize the parameters to minimize the error between observed $y$ and predicted $y$. These methods only return single best value for parameters.</p>

<p><img src="/images/p4/linear.png" width="300" class="center" />
Image credits: Wikipedia</p>

<p><strong>Bayesian Approach</strong></p>

<p>The same problem can be stated under probablistic framework. We can obtain best values of $ \alpha\ $  and $ \beta\ $ along with their uncertainity estimations. Probablistically linear regression can be explained as :</p>

\[y \sim N(\mu=\alpha+\beta x, \sigma=\varepsilon)\]

<p>$y$ is observed as a Gaussian distribution with mean $ \mu\ $ and standard deviation $ \sigma\ $. Unlike OLS regression, here it is normally distibuted. Since we do not know the values of $ \alpha\ $  , $ \beta\ $ and $ \epsilon\ $, we have to set prior distributions for them.</p>

\[\begin{array}{l}{\alpha \sim N\left(\mu_{\alpha}, \sigma_{\alpha}\right)} \\ {\beta \sim N\left(\mu_{\beta}, \sigma_{\beta}\right)} \\ {\varepsilon \sim U\left(0, h_{s}\right)}\end{array}\]

<p><img src="/images/p4/bayesian.PNG" width="300" class="center" />
Image credits: Osvaldo Martin’s book: Bayesian Analysis with Python</p>

<p>In this post, I’m going to demonstrate very simple linear regression problem with both OLS and bayesian approach. We will use <a href="https://docs.pymc.io/">PyMC3 package</a>. PyMC3 is a Python package for Bayesian statistical modeling and probabilistic machine learning.</p>

<h3 id="import-basic-modules">Import basic modules</h3>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="n">np</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="n">plt</span>
<span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="n">pd</span>
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="n">sns</span>

</code></pre></div></div>

<h3 id="generate-linear-artificial-data">Generate linear artificial data</h3>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">rng</span> <span class="o">=</span> <span class="n">np</span><span class="p">.</span><span class="n">random</span><span class="p">.</span><span class="n">RandomState</span><span class="p">(</span><span class="mi">1</span><span class="p">)</span>
<span class="n">x</span> <span class="o">=</span> <span class="mi">10</span> <span class="o">*</span> <span class="n">rng</span><span class="p">.</span><span class="n">rand</span><span class="p">(</span><span class="mi">50</span><span class="p">)</span>
<span class="n">y</span> <span class="o">=</span> <span class="mi">2</span> <span class="o">*</span> <span class="n">x</span> <span class="o">-</span> <span class="mi">5</span> <span class="o">+</span> <span class="mi">2</span><span class="o">*</span><span class="n">rng</span><span class="p">.</span><span class="n">randn</span><span class="p">(</span><span class="mi">50</span><span class="p">)</span>
<span class="n">x</span> <span class="o">=</span> <span class="n">x</span><span class="p">.</span><span class="n">reshape</span><span class="p">(</span><span class="o">-</span><span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span>
<span class="n">y</span> <span class="o">=</span> <span class="n">y</span><span class="p">.</span><span class="n">reshape</span><span class="p">(</span><span class="o">-</span><span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span>

<span class="n">plt</span><span class="p">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">y</span><span class="p">)</span>
</code></pre></div></div>

<p><img src="/images/p4/output_4_1.png" /></p>

<h3 id="create-pymc3-model">Create PyMC3 model</h3>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kn">import</span> <span class="nn">pymc3</span> <span class="k">as</span> <span class="n">pm</span>
<span class="k">print</span><span class="p">(</span><span class="s">'Running on the PyMC3 v{}'</span><span class="p">.</span><span class="nb">format</span><span class="p">(</span><span class="n">pm</span><span class="p">.</span><span class="n">__version__</span><span class="p">))</span>
<span class="n">basic_model</span> <span class="o">=</span>  <span class="n">pm</span><span class="p">.</span><span class="n">Model</span><span class="p">()</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>Running on the PyMC3 v3.6
</code></pre></div></div>

<h3 id="define-model-parameters">Define model parameters</h3>

<p>Context is created for defining model parameters using <code class="language-plaintext highlighter-rouge">with</code> statement. Using context makes it easy to assign parameters to model.</p>

<p>Distributions for  $ \alpha\ $  , $ \beta\ $ and $ \epsilon\ $ are defined. $ \mu\ $ is a deterministic variable which calculated using line equation.</p>

<p><code class="language-plaintext highlighter-rouge">Ylikelihood</code> is a likelihood parameter which is defined ny Normal distribution with $ \mu\ $ and $ \sigma\ $. Observed values are also passed along with distribution.</p>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="k">with</span> <span class="n">basic_model</span> <span class="k">as</span> <span class="n">bm</span><span class="p">:</span>

    <span class="c1">#Priors
</span>    <span class="n">alpha</span> <span class="o">=</span> <span class="n">pm</span><span class="p">.</span><span class="n">Normal</span><span class="p">(</span><span class="s">'alpha'</span><span class="p">,</span> <span class="n">mu</span><span class="o">=</span><span class="mi">0</span><span class="p">,</span> <span class="n">sd</span><span class="o">=</span><span class="mi">10</span><span class="p">)</span>
    <span class="n">beta</span> <span class="o">=</span> <span class="n">pm</span><span class="p">.</span><span class="n">Normal</span><span class="p">(</span><span class="s">'beta'</span><span class="p">,</span> <span class="n">mu</span><span class="o">=</span><span class="mi">0</span><span class="p">,</span> <span class="n">sd</span><span class="o">=</span><span class="mi">10</span><span class="p">)</span>
    <span class="n">sigma</span> <span class="o">=</span> <span class="n">pm</span><span class="p">.</span><span class="n">HalfNormal</span><span class="p">(</span><span class="s">'sigma'</span><span class="p">,</span> <span class="n">sd</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>

    <span class="c1"># Deterministics
</span>    <span class="n">mu</span> <span class="o">=</span> <span class="n">alpha</span> <span class="o">+</span> <span class="n">beta</span><span class="o">*</span><span class="n">x</span>
    
    <span class="c1"># Likelihood 
</span>    <span class="n">Ylikelihood</span> <span class="o">=</span> <span class="n">pm</span><span class="p">.</span><span class="n">Normal</span><span class="p">(</span><span class="s">'Ylikelihood'</span><span class="p">,</span> <span class="n">mu</span><span class="o">=</span><span class="n">mu</span><span class="p">,</span> <span class="n">sd</span><span class="o">=</span><span class="n">sigma</span><span class="p">,</span> <span class="n">observed</span><span class="o">=</span><span class="n">y</span><span class="p">)</span>
</code></pre></div></div>

<h3 id="sampling-from-posterior">Sampling from posterior</h3>

<p>As model is defined completely, now we can sample from posterior. PyMC3 automatically chooses appropriate model depending on the type of data. In our case of continuous data, NUTS is used.</p>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code> <span class="n">trace</span> <span class="o">=</span> <span class="n">pm</span><span class="p">.</span><span class="n">sample</span><span class="p">(</span><span class="n">draws</span><span class="o">=</span><span class="mi">2000</span><span class="p">,</span><span class="n">model</span><span class="o">=</span><span class="n">bm</span><span class="p">)</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>Auto-assigning NUTS sampler...
Initializing NUTS using jitter+adapt_diag...
Sequential sampling (2 chains in 1 job)
NUTS: [sigma, beta, alpha]
100%|██████████| 2500/2500 [00:03&lt;00:00, 770.37it/s]
100%|██████████| 2500/2500 [00:03&lt;00:00, 721.84it/s]
The acceptance probability does not match the target. It is 0.8850329863869828, but should be close to 0.8. Try to increase the number of tuning steps.
</code></pre></div></div>

<h3 id="trace-summary-and-plots">Trace summary and plots</h3>
<p>Traceplots plots samples histograms and values.</p>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">pm</span><span class="p">.</span><span class="n">traceplot</span><span class="p">(</span><span class="n">trace</span><span class="p">)</span>
</code></pre></div></div>

<p><img src="/images/p4/output_12_1.png" /></p>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="k">print</span><span class="p">(</span><span class="n">pm</span><span class="p">.</span><span class="n">summary</span><span class="p">(</span><span class="n">trace</span><span class="p">).</span><span class="nb">round</span><span class="p">(</span><span class="mi">2</span><span class="p">))</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>       mean    sd  mc_error  hpd_2.5  hpd_97.5    n_eff  Rhat
alpha -5.00  0.48      0.01    -5.93     -4.05  1619.65   1.0
beta   2.05  0.09      0.00     1.89      2.23  1583.34   1.0
sigma  1.83  0.18      0.00     1.49      2.18  2254.55   1.0
</code></pre></div></div>

<h3 id="checking-autocorrelation">Checking autocorrelation</h3>

<p>Bar plot of the autocorrelation function for a trace can be plotted using <a href="https://docs.pymc.io/api/plots.html">pymc3.plots.autocorrplot</a>.</p>

<p>Autocorrelation dictates the amount of time you have to wait for convergence. If autocorrelation is high, you will have to use a longer burn-in. Low autocorrelation means good exploration.</p>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">pm</span><span class="p">.</span><span class="n">autocorrplot</span><span class="p">(</span><span class="n">trace</span><span class="p">)</span>
</code></pre></div></div>

<p><img src="/images/p4/output_15_1.png" /></p>

<h3 id="comparing-parameters-with-simple-linear-regression-ols">Comparing parameters with Simple Linear Regression (OLS)</h3>

<p>Parameters can be cross checked using Simple Linear Regression.</p>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code>
<span class="kn">from</span> <span class="nn">sklearn.linear_model</span> <span class="kn">import</span> <span class="n">LinearRegression</span>
<span class="n">lm</span> <span class="o">=</span> <span class="n">LinearRegression</span><span class="p">()</span>
<span class="n">ypred</span> <span class="o">=</span>  <span class="n">lm</span><span class="p">.</span><span class="n">fit</span><span class="p">(</span><span class="n">x</span><span class="p">,</span><span class="n">y</span><span class="p">).</span><span class="n">predict</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
<span class="n">plt</span><span class="p">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">x</span><span class="p">,</span><span class="n">y</span><span class="p">)</span>
<span class="n">plt</span><span class="p">.</span><span class="n">plot</span><span class="p">(</span><span class="n">x</span><span class="p">,</span><span class="n">ypred</span><span class="p">)</span>
<span class="n">legend_title</span> <span class="o">=</span> <span class="s">'Simple Linear Regression</span><span class="se">\n</span><span class="s"> {} + {}*x'</span><span class="p">.</span><span class="nb">format</span><span class="p">(</span><span class="nb">round</span><span class="p">(</span><span class="n">lm</span><span class="p">.</span><span class="n">intercept_</span><span class="p">[</span><span class="mi">0</span><span class="p">],</span><span class="mi">2</span><span class="p">),</span><span class="nb">round</span><span class="p">(</span><span class="n">lm</span><span class="p">.</span><span class="n">coef_</span><span class="p">[</span><span class="mi">0</span><span class="p">][</span><span class="mi">0</span><span class="p">],</span><span class="mi">2</span><span class="p">))</span>
<span class="n">legend</span> <span class="o">=</span> <span class="n">plt</span><span class="p">.</span><span class="n">legend</span><span class="p">(</span><span class="n">loc</span><span class="o">=</span><span class="s">'upper left'</span><span class="p">,</span> <span class="n">frameon</span><span class="o">=</span><span class="bp">False</span><span class="p">,</span> <span class="n">title</span><span class="o">=</span><span class="n">legend_title</span><span class="p">)</span>
<span class="n">plt</span><span class="p">.</span><span class="n">title</span><span class="p">(</span><span class="s">"Simple Linear Regression"</span><span class="p">)</span>
<span class="n">plt</span><span class="p">.</span><span class="n">show</span><span class="p">()</span>

</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>No handles with labels found to put in legend.
</code></pre></div></div>

<p><img src="/images/p4/output_17_1.png" /></p>

<p>Parameters are almost similar for both pyMc3 and Simple Linear Regression</p>

<p><strong>Intercept</strong></p>

<p>OLS: -5.0
PyMc3: -5.0</p>

<p><strong>Coefficient</strong></p>

<p>OLS: 2.03
PyMc3: 2.05</p>

<h3 id="plotting-traces">Plotting traces</h3>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">plt</span><span class="p">.</span><span class="n">plot</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="s">'b.'</span><span class="p">);</span>

<span class="n">idx</span> <span class="o">=</span> <span class="nb">range</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="nb">len</span><span class="p">(</span><span class="n">trace</span><span class="p">[</span><span class="s">'alpha'</span><span class="p">]),</span> <span class="mi">10</span><span class="p">)</span>
<span class="n">alpha_m</span> <span class="o">=</span> <span class="n">trace</span><span class="p">[</span><span class="s">'alpha'</span><span class="p">].</span><span class="n">mean</span><span class="p">()</span>
<span class="n">beta_m</span> <span class="o">=</span> <span class="n">trace</span><span class="p">[</span><span class="s">'beta'</span><span class="p">].</span><span class="n">mean</span><span class="p">()</span>

<span class="n">plt</span><span class="p">.</span><span class="n">plot</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">trace</span><span class="p">[</span><span class="s">'alpha'</span><span class="p">][</span><span class="n">idx</span><span class="p">]</span> <span class="o">+</span> <span class="n">trace</span><span class="p">[</span><span class="s">'beta'</span><span class="p">][</span><span class="n">idx</span><span class="p">]</span> <span class="o">*</span><span class="n">x</span><span class="p">,</span> <span class="n">c</span><span class="o">=</span><span class="s">'gray'</span><span class="p">,</span> <span class="n">alpha</span><span class="o">=</span><span class="mf">0.2</span><span class="p">);</span>
<span class="n">plt</span><span class="p">.</span><span class="n">plot</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">alpha_m</span> <span class="o">+</span> <span class="n">beta_m</span> <span class="o">*</span> <span class="n">x</span><span class="p">,</span> <span class="n">c</span><span class="o">=</span><span class="s">'k'</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="s">'y = {:.2f} + {:.2f}* x'</span><span class="p">.</span><span class="nb">format</span><span class="p">(</span><span class="n">alpha_m</span><span class="p">,</span> <span class="n">beta_m</span><span class="p">))</span>
<span class="n">plt</span><span class="p">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s">'$x$'</span><span class="p">,</span> <span class="n">fontsize</span><span class="o">=</span><span class="mi">16</span><span class="p">)</span>
<span class="n">plt</span><span class="p">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s">'$y$'</span><span class="p">,</span> <span class="n">fontsize</span><span class="o">=</span><span class="mi">16</span><span class="p">,</span> <span class="n">rotation</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span>
<span class="n">plt</span><span class="p">.</span><span class="n">legend</span><span class="p">(</span><span class="n">loc</span><span class="o">=</span><span class="mi">2</span><span class="p">,</span> <span class="n">fontsize</span><span class="o">=</span><span class="mi">14</span><span class="p">)</span>
<span class="n">plt</span><span class="p">.</span><span class="n">title</span><span class="p">(</span><span class="s">"Traces"</span><span class="p">)</span>
<span class="n">plt</span><span class="p">.</span><span class="n">show</span><span class="p">()</span>
</code></pre></div></div>

<p><img src="/images/p4/output_20_0.png" /></p>

<h3 id="posterior-plots">Posterior Plots</h3>
<p>Plot Posterior densities in style of John K. Kruschke’s book.</p>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">pm</span><span class="p">.</span><span class="n">plots</span><span class="p">.</span><span class="n">plot_posterior</span><span class="p">(</span><span class="n">trace</span><span class="p">)</span>
</code></pre></div></div>

<p><img src="/images/p4/output_22_1.png" /></p>

<h3 id="forest-plots">Forest Plots</h3>
<p>Generates a “forest plot” of 100*(1-alpha)% credible intervals from a trace or list of traces. 
It also shows R-hat - The Gelman and Rubin diagnostic which is used to check the convergence of multiple mcmc chains run in parallel</p>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">pm</span><span class="p">.</span><span class="n">plots</span><span class="p">.</span><span class="n">forestplot</span><span class="p">(</span><span class="n">trace</span><span class="p">)</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>GridSpec(1, 2, width_ratios=[3, 1])
</code></pre></div></div>

<p><img src="/images/p4/output_24_1.png" /></p>

<h3 id="plotting-energy-distributions">Plotting energy distributions</h3>
<p>Plot energy transition distribution and marginal energy distribution in order to diagnose poor exploration by HMC algorithms. 
For high-dimensional models it becomes cumbersome to look at all parameter’s traces, hence Energy plot is used to assess problems of convergence.</p>

<p>If you have the energy transition distribution much more narrow than energy distribution, it means you dont have enough energy to explore the whole parameter space and your posterior estimation is likely biased.</p>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">pm</span><span class="p">.</span><span class="n">plots</span><span class="p">.</span><span class="n">energyplot</span><span class="p">(</span><span class="n">trace</span><span class="p">)</span>
</code></pre></div></div>

<p><img src="/images/p4/output_26_1.png" /></p>

<h3 id="density-plots">Density Plots</h3>
<p>Generates KDE plots for continuous variables. Plots are truncated at their 100*(1-alpha)% credible intervals.</p>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">pm</span><span class="p">.</span><span class="n">plots</span><span class="p">.</span><span class="n">densityplot</span><span class="p">(</span><span class="n">trace</span><span class="p">)</span>
</code></pre></div></div>

<p><img src="/images/p4/output_28_1.png" /></p>

<h3 id="sampling-from-posterior-1">Sampling from Posterior</h3>

<p>Posterior predictive checks (PPCs) are a great way to validate a model. The idea is to generate data from the model using parameters from draws from the posterior.</p>

<p>We will draw samples from the observed model.</p>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">ypred</span> <span class="o">=</span> <span class="n">pm</span><span class="p">.</span><span class="n">sampling</span><span class="p">.</span><span class="n">sample_posterior_predictive</span><span class="p">(</span><span class="n">model</span><span class="o">=</span><span class="n">bm</span><span class="p">,</span><span class="n">trace</span><span class="o">=</span><span class="n">trace</span><span class="p">,</span> <span class="n">samples</span><span class="o">=</span><span class="mi">500</span><span class="p">)</span>
<span class="n">y_sample_posterior_predictive</span> <span class="o">=</span> <span class="n">np</span><span class="p">.</span><span class="n">asarray</span><span class="p">(</span><span class="n">ypred</span><span class="p">[</span><span class="s">'Ylikelihood'</span><span class="p">])</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>100%|██████████| 500/500 [00:00&lt;00:00, 1090.41it/s]
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">_</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">plt</span><span class="p">.</span><span class="n">subplots</span><span class="p">()</span>
<span class="n">ax</span><span class="p">.</span><span class="n">hist</span><span class="p">([</span><span class="n">n</span><span class="p">.</span><span class="n">mean</span><span class="p">()</span> <span class="k">for</span> <span class="n">n</span> <span class="ow">in</span> <span class="n">y_sample_posterior_predictive</span><span class="p">],</span> <span class="n">bins</span><span class="o">=</span><span class="mi">19</span><span class="p">,</span> <span class="n">alpha</span><span class="o">=</span><span class="mf">0.5</span><span class="p">)</span>
<span class="n">ax</span><span class="p">.</span><span class="n">axvline</span><span class="p">(</span><span class="n">y</span><span class="p">.</span><span class="n">mean</span><span class="p">())</span>
<span class="n">ax</span><span class="p">.</span><span class="nb">set</span><span class="p">(</span><span class="n">title</span><span class="o">=</span><span class="s">'Posterior predictive of the mean'</span><span class="p">,</span> <span class="n">xlabel</span><span class="o">=</span><span class="s">'mean(x)'</span><span class="p">,</span> <span class="n">ylabel</span><span class="o">=</span><span class="s">'Frequency'</span><span class="p">);</span>
</code></pre></div></div>

<p><img src="/images/p4/output_31_0.png" /></p>

<h3 id="plotting-hpd-intervals">Plotting HPD intervals</h3>

<p>We can plot credible intervals to see unobserved parameter values that fall with a particular subjective probability. The HPD has the nice property that any point <strong>within</strong> the interval has a higher density than any other point outside. To calculate highest posterior density (HPD) of array for given alpha, we use a function given by PyMC3 :  <a href="https://docs.pymc.io/api/stats.html">pymc3.stats.hpd()</a></p>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">sig0</span> <span class="o">=</span> <span class="n">pm</span><span class="p">.</span><span class="n">hpd</span><span class="p">(</span><span class="n">y_sample_posterior_predictive</span><span class="p">,</span> <span class="n">alpha</span><span class="o">=</span><span class="mf">0.5</span><span class="p">)</span>
<span class="n">sig1</span> <span class="o">=</span> <span class="n">pm</span><span class="p">.</span><span class="n">hpd</span><span class="p">(</span><span class="n">y_sample_posterior_predictive</span><span class="p">,</span> <span class="n">alpha</span><span class="o">=</span><span class="mf">0.05</span><span class="p">)</span>

<span class="c1">#removing extra dimension
</span><span class="n">sig0</span> <span class="o">=</span> <span class="n">np</span><span class="p">.</span><span class="n">squeeze</span><span class="p">(</span><span class="n">sig0</span><span class="p">)</span>
<span class="n">sig1</span> <span class="o">=</span> <span class="n">np</span><span class="p">.</span><span class="n">squeeze</span><span class="p">(</span><span class="n">sig1</span><span class="p">)</span>

<span class="c1">#Reshaping and sorting
</span><span class="n">inds</span> <span class="o">=</span> <span class="n">x</span><span class="p">.</span><span class="n">ravel</span><span class="p">().</span><span class="n">argsort</span><span class="p">()</span>    
<span class="n">x_ord</span> <span class="o">=</span> <span class="n">x</span><span class="p">.</span><span class="n">ravel</span><span class="p">()[</span><span class="n">inds</span><span class="p">].</span><span class="n">reshape</span><span class="p">(</span><span class="o">-</span><span class="mi">1</span><span class="p">)</span>

<span class="n">y</span><span class="o">=</span> <span class="n">y</span><span class="p">[</span><span class="n">inds</span><span class="p">]</span>
<span class="n">sig0ord</span><span class="o">=</span> <span class="n">sig0</span><span class="p">[</span><span class="n">inds</span><span class="p">]</span>
<span class="n">sig1ord</span> <span class="o">=</span> <span class="n">sig1</span><span class="p">[</span><span class="n">inds</span><span class="p">]</span>
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code>
<span class="n">pal</span> <span class="o">=</span> <span class="n">sns</span><span class="p">.</span><span class="n">color_palette</span><span class="p">(</span><span class="s">'Purples'</span><span class="p">)</span>
<span class="c1">#plt.plot(x, y, 'b.')
</span><span class="n">plt</span><span class="p">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">x_ord</span><span class="p">,</span><span class="n">y</span><span class="p">)</span>
<span class="n">plt</span><span class="p">.</span><span class="n">plot</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">alpha_m</span> <span class="o">+</span> <span class="n">beta_m</span> <span class="o">*</span> <span class="n">x</span><span class="p">,</span> <span class="n">c</span><span class="o">=</span><span class="s">'k'</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="s">'y = {:.2f} + {:.2f}* x'</span><span class="p">.</span><span class="nb">format</span><span class="p">(</span><span class="n">alpha_m</span><span class="p">,</span> <span class="n">beta_m</span><span class="p">))</span>
<span class="n">plt</span><span class="p">.</span><span class="n">fill_between</span><span class="p">(</span><span class="n">x_ord</span><span class="p">,</span> <span class="n">sig0ord</span><span class="p">[:,</span><span class="mi">0</span><span class="p">],</span> <span class="n">sig0ord</span><span class="p">[:,</span><span class="mi">1</span><span class="p">],</span> <span class="n">color</span><span class="o">=</span><span class="s">'red'</span><span class="p">,</span><span class="n">alpha</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span><span class="n">label</span><span class="o">=</span><span class="s">"50% interval"</span><span class="p">)</span>
<span class="n">plt</span><span class="p">.</span><span class="n">fill_between</span><span class="p">(</span><span class="n">x_ord</span><span class="p">,</span> <span class="n">sig1ord</span><span class="p">[:,</span><span class="mi">0</span><span class="p">],</span> <span class="n">sig1ord</span><span class="p">[:,</span><span class="mi">1</span><span class="p">],</span> <span class="n">color</span><span class="o">=</span><span class="s">'gray'</span><span class="p">,</span><span class="n">alpha</span><span class="o">=</span><span class="mf">0.5</span><span class="p">,</span><span class="n">label</span><span class="o">=</span><span class="s">"95% interval"</span><span class="p">)</span>
<span class="n">plt</span><span class="p">.</span><span class="n">legend</span><span class="p">()</span>
<span class="n">plt</span><span class="p">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s">'$x$'</span><span class="p">,</span> <span class="n">fontsize</span><span class="o">=</span><span class="mi">16</span><span class="p">)</span>
<span class="n">plt</span><span class="p">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s">'$y$'</span><span class="p">,</span> <span class="n">fontsize</span><span class="o">=</span><span class="mi">16</span><span class="p">,</span> <span class="n">rotation</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span>
<span class="n">plt</span><span class="p">.</span><span class="n">title</span><span class="p">(</span><span class="s">"HPD Plot"</span><span class="p">)</span>
<span class="n">plt</span><span class="p">.</span><span class="n">show</span><span class="p">()</span>
</code></pre></div></div>

<p><img src="/images/p4/output_34_0.png" /></p>

<p>Similarily using ‘posterior_predictive’ samples, we can get various percentile values to plot.</p>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">dfp</span> <span class="o">=</span> <span class="n">np</span><span class="p">.</span><span class="n">percentile</span><span class="p">(</span><span class="n">y_sample_posterior_predictive</span><span class="p">,[</span><span class="mf">2.5</span><span class="p">,</span><span class="mi">25</span><span class="p">,</span><span class="mi">50</span><span class="p">,</span><span class="mi">70</span><span class="p">,</span><span class="mf">97.5</span><span class="p">],</span><span class="n">axis</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span>
<span class="n">dfp</span> <span class="o">=</span> <span class="n">np</span><span class="p">.</span><span class="n">squeeze</span><span class="p">(</span><span class="n">dfp</span><span class="p">)</span>
<span class="n">dfp</span> <span class="o">=</span> <span class="n">dfp</span><span class="p">[:,</span><span class="n">inds</span><span class="p">]</span>

<span class="n">ymean</span> <span class="o">=</span> <span class="n">y_sample_posterior_predictive</span><span class="p">.</span><span class="n">mean</span><span class="p">(</span><span class="n">axis</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span>
<span class="n">ymean</span> <span class="o">=</span><span class="n">ymean</span><span class="p">[</span><span class="n">inds</span><span class="p">]</span>
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code>
<span class="n">pal</span> <span class="o">=</span> <span class="n">sns</span><span class="p">.</span><span class="n">color_palette</span><span class="p">(</span><span class="s">'Purples'</span><span class="p">)</span>
<span class="n">plt</span><span class="p">.</span><span class="n">rcParams</span><span class="p">[</span><span class="s">'axes.facecolor'</span><span class="p">]</span> <span class="o">=</span> <span class="s">'white'</span>
<span class="n">plt</span><span class="p">.</span><span class="n">rcParams</span><span class="p">[</span><span class="s">"axes.linewidth"</span><span class="p">]</span>  <span class="o">=</span> <span class="mf">1.25</span>
<span class="n">plt</span><span class="p">.</span><span class="n">rcParams</span><span class="p">[</span><span class="s">"axes.edgecolor"</span><span class="p">]</span> <span class="o">=</span> <span class="s">"0.15"</span>


<span class="n">fig</span> <span class="o">=</span> <span class="n">plt</span><span class="p">.</span><span class="n">figure</span><span class="p">(</span><span class="n">dpi</span><span class="o">=</span><span class="mi">100</span><span class="p">)</span>
<span class="n">ax</span> <span class="o">=</span> <span class="n">fig</span><span class="p">.</span><span class="n">add_subplot</span><span class="p">(</span><span class="mi">111</span><span class="p">)</span>
<span class="n">plt</span><span class="p">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">x_ord</span><span class="p">,</span><span class="n">y</span><span class="p">,</span><span class="n">s</span><span class="o">=</span><span class="mi">10</span><span class="p">,</span><span class="n">label</span><span class="o">=</span><span class="s">'observed'</span><span class="p">)</span>
<span class="n">ax</span><span class="p">.</span><span class="n">plot</span><span class="p">(</span><span class="n">x_ord</span><span class="p">,</span><span class="n">ymean</span><span class="p">,</span><span class="n">c</span><span class="o">=</span><span class="n">pal</span><span class="p">[</span><span class="mi">5</span><span class="p">],</span><span class="n">label</span><span class="o">=</span><span class="s">'posterior mean'</span><span class="p">,</span><span class="n">alpha</span><span class="o">=</span><span class="mf">0.5</span><span class="p">)</span>
<span class="n">ax</span><span class="p">.</span><span class="n">plot</span><span class="p">(</span><span class="n">x_ord</span><span class="p">,</span><span class="n">dfp</span><span class="p">[</span><span class="mi">2</span><span class="p">,:],</span><span class="n">alpha</span><span class="o">=</span><span class="mf">0.75</span><span class="p">,</span><span class="n">color</span><span class="o">=</span><span class="n">pal</span><span class="p">[</span><span class="mi">3</span><span class="p">],</span><span class="n">label</span><span class="o">=</span><span class="s">'posterior median'</span><span class="p">)</span>
<span class="n">ax</span><span class="p">.</span><span class="n">fill_between</span><span class="p">(</span><span class="n">x_ord</span><span class="p">,</span><span class="n">dfp</span><span class="p">[</span><span class="mi">0</span><span class="p">,:],</span><span class="n">dfp</span><span class="p">[</span><span class="mi">4</span><span class="p">,:],</span><span class="n">alpha</span><span class="o">=</span><span class="mf">0.5</span><span class="p">,</span><span class="n">color</span><span class="o">=</span><span class="n">pal</span><span class="p">[</span><span class="mi">1</span><span class="p">],</span><span class="n">label</span><span class="o">=</span><span class="s">'CR 95%'</span><span class="p">)</span>
<span class="n">ax</span><span class="p">.</span><span class="n">fill_between</span><span class="p">(</span><span class="n">x_ord</span><span class="p">,</span><span class="n">dfp</span><span class="p">[</span><span class="mi">1</span><span class="p">,:],</span><span class="n">dfp</span><span class="p">[</span><span class="mi">3</span><span class="p">,:],</span><span class="n">alpha</span><span class="o">=</span><span class="mf">0.4</span><span class="p">,</span><span class="n">color</span><span class="o">=</span><span class="n">pal</span><span class="p">[</span><span class="mi">2</span><span class="p">],</span><span class="n">label</span><span class="o">=</span><span class="s">'CR 50%'</span><span class="p">)</span>
<span class="n">ax</span><span class="p">.</span><span class="n">legend</span><span class="p">()</span>
<span class="n">plt</span><span class="p">.</span><span class="n">legend</span><span class="p">(</span><span class="n">frameon</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>
<span class="n">plt</span><span class="p">.</span><span class="n">show</span><span class="p">()</span>

</code></pre></div></div>

<p><img src="/images/p4/output_37_0.png" /></p>

<h3 id="source">Source</h3>

<p>You can find jupyter notebook <a href="https://github.com/ostwalprasad/ostwalprasad.github.io/blob/master/jupyterbooks/2019-04-17-Bayesian Linear Regression using PyMC3.ipynb">here</a></p>


  </div>
  

	<br /> 

	<strong>Want to build own site like this within 5 minutes?<br/>  Fork this <a href = "https://github.com/ostwalprasad/ostwalprasad.github.io">repository</a> and follow this nice <a href = "https://deanattali.com/beautiful-jekyll/getstarted">tutorial</a> to get yourname.github.io website!</strong>
	<br /> 
	<br /> 
	<br /> 
	
	<div class="social-buttons">

<hr size="5" width="100%" align="left" color="black">
		<h4>
			Don't swear, just share and comment:
		</h4>
    <a href="https://facebook.com/sharer.php?u=http://ostwalprasad.github.io/machine-learning/Bayesian-Linear-Regression-using-PyMC3.html" 
    rel="nofollow" target="_blank" title="Share on Facebook" class="z-2 z-h social fb">
    	<i class="fa fa-facebook"></i> Facebook
    </a>
    
    <a href="https://twitter.com/intent/tweet?text=Bayesian Linear Regression using PyMC3 &url=http://ostwalprasad.github.io/machine-learning/Bayesian-Linear-Regression-using-PyMC3.html" 
    rel="nofollow" target="_blank" title="Share on Twitter" class="z-2 z-h social tw">
    	<i class="fa fa-twitter"></i> Twitter</a>
    
    <a href="http://www.linkedin.com/shareArticle?mini=true&url=http://ostwalprasad.github.io/machine-learning/Bayesian-Linear-Regression-using-PyMC3.html&title=Bayesian Linear Regression using PyMC3 &summary=&source=http://ostwalprasad.github.io" 
    rel="nofollow" target="_blank" title="Share On LinkedIn" class="z-2 z-h social li">
    	<i class="fa fa-linkedin"></i> LinkedIn
    </a>
    
    <a href="http://www.reddit.com/submit?url=http://ostwalprasad.github.io/machine-learning/Bayesian-Linear-Regression-using-PyMC3.html&title=Bayesian Linear Regression using PyMC3 " 
    rel="nofollow" target="_blank" title="Share On Reddit" class="z-2 z-h social rd">
    	<i class="fa fa-reddit-alien"></i> Reddit
    </a>

</div>
<div id="disqus_thread"></div>
  <script>
    var disqus_config = function () {
      this.page.url = 'http://ostwalprasad.github.io/machine-learning/Bayesian-Linear-Regression-using-PyMC3.html';
      this.page.identifier = 'http://ostwalprasad.github.io/machine-learning/Bayesian-Linear-Regression-using-PyMC3.html';
    };

    (function() {
      var d = document, s = d.createElement('script');

      s.src = 'https://ostwalprasad-github-io.disqus.com/embed.js';

      s.setAttribute('data-timestamp', +new Date());
      (d.head || d.body).appendChild(s);
    })();
  </script>
  <noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript" rel="nofollow">comments powered by Disqus.</a></noscript><a class="u-url" href="/machine-learning/Bayesian-Linear-Regression-using-PyMC3.html" hidden></a>
</article>

	  <div >
	


</div>
    </div>

  </body>
</html>



# Hello
```powershell
Get-Command -Name Clear-Host
```
<pre class="r"><code>install.packages(c(&quot;insight&quot;, &quot;bayestestR&quot;, &quot;parameters&quot;))</code></pre>
@octocat :+1: This PR looks great - it's ready to merge! :shipit:

Rendered emoji
My first github pages
(like ~~this~~) 
```
import numpy as np
```
```ruby
require 'redcarpet'
markdown = Redcarpet.new("Hello World!")
puts markdown.to_html
```
```
function test() {
  console.log("notice the blank line before this function?");
}
```
It's very easy to make some words **bold** and other words *italic* with Markdown. You can even [link to Google!](http://google.com)

Headers

# This is an <h1> tag
## This is an <h2> tag
###### This is an <h6> tag
Inline code

I think you should use an
`<numpy>` element here instead.
```javascript
function fancyAlert(arg) {
  if(arg) {
    $.facebox({div:'#foo'})
  }
}
```
First Header | Second Header
------------ | -------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column
  
Username @mentions  
