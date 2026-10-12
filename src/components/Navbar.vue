<template>
	<!-- navbar start -->
	<nav id="navbar" class="navbar navbar-expand-lg navbar-light border-bottom border-1">
	    <div class="container">
	    	<!-- logo -->
	        <a class="navbar-brand" href="#about">LOISA</a>

	        <!-- Desktop Menu -->
	        <div class="d-none d-lg-flex ms-auto">
	        	<ul class="navbar-nav">
	               <li class="nav-item">
	                   <a class="nav-link active" aria-current="page" href="#landing">About</a>
	               </li>
	               <li class="nav-item ms-4">
	                   <a class="nav-link" href="#education">Education</a>
	               </li>
	               <li class="nav-item ms-4">
	                   <a class="nav-link" href="#projects">Projects</a>
	               </li>
	               <li class="nav-item ms-4">
	                   <a class="nav-link" href="#tools">Tools</a>
	               </li>
	               <li class="nav-item ms-4">
	                   <a class="nav-link" href="#contact">Contact</a>
	               </li>
	           </ul>
	        </div>

	        <!-- Mobile Hamburger -->
	        <button class="navbar-toggler"
	            type="button"
	            data-bs-toggle="offcanvas"
	            data-bs-target="#mobileMenu"
	            aria-controls="mobileMenu"
	            aria-expanded="false"
	            aria-label="Toggle navigation">
	            <span class="navbar-toggler-icon"></span>
	        </button>

		    <!-- Navigation Links Mobile -->
		    <div class="offcanvas offcanvas-end d-lg-none" tabindex="-1" id="mobileMenu">
		    	<div class="offcanvas-header">
	               <h5 class="fw-bold ms-2">Menu</h5>
	               <button type="button"
	                       class="btn-close fs-4"
	                       data-bs-dismiss="offcanvas">
	               </button>
           		</div>
           		<div class="offcanvas-body">
           			<ul class="navbar-nav m-3">
           			    <li class="nav-item bi"><a class="nav-link active bi-file-person" aria-current="page" href="#landing">   About</a></li>
           			    <li class="nav-item"><a class="nav-link bi bi-mortarboard" href="#education"> Education</a></li>
           			    <li class="nav-item"><a class="nav-link bi bi-laptop" href="#projects"> Projects</a></li>
           			    <li class="nav-item"><a class="nav-link bi bi-tools" href="#tools"> Tools</a></li>
           			    <li class="nav-item"><a class="nav-link bi bi-telephone" href="#contact"> Contact</a></li>
           			</ul>
           		</div>
		    </div>
		    <!-- Navigation Links Mobile End -->
	   </div>
	</nav>
	<!-- navbar end -->
</template>