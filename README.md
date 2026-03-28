<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LAUMSA-SCOME Library - Ladoke Akintola University Medical Student Resource Hub</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    },
                    colors: {
                        medical: {
                            50: '#f0f9ff',
                            100: '#e0f2fe',
                            500: '#0ea5e9',
                            600: '#0284c7',
                            700: '#0369a1',
                            800: '#075985',
                            900: '#0c4a6e',
                        },
                        teal: {
                            50: '#f0fdfa',
                            500: '#14b8a6',
                            600: '#0d9488',
                        },
                        lautech: {
                            600: '#166534',
                            700: '#14532d',
                        }
                    }
                }
            }
        }
    </script>
    <style>
        .glass-effect {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
        }
        .resource-card {
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .resource-card:hover {
            transform: translateY(-4px);
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
        }
        .senior-card {
            transition: all 0.3s ease;
        }
        .senior-card:hover {
            transform: scale(1.02);
        }
        .upload-zone {
            border: 2px dashed #cbd5e1;
            transition: all 0.3s ease;
        }
        .upload-zone.dragover {
            border-color: #166534;
            background-color: #f0fdf4;
        }
        .animate-fade-in {
            animation: fadeIn 0.5s ease-in;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .tab-active {
            border-bottom: 2px solid #166534;
            color: #166534;
        }
        .category-pill {
            transition: all 0.2s ease;
        }
        .category-pill:hover {
            transform: translateY(-2px);
        }
        .category-pill.active {
            background-color: #166534;
            color: white;
        }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 font-sans antialiased">

    <!-- Navigation -->
    <nav class="fixed w-full z-50 glass-effect border-b border-slate-200">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between h-16 items-center">
                <div class="flex items-center gap-3 cursor-pointer" onclick="showSection('home')">
                    <div class="w-10 h-10 bg-gradient-to-br from-lautech-600 to-teal-500 rounded-xl flex items-center justify-center text-white font-bold text-xl shadow-lg">
                        <i class="fas fa-book-medical"></i>
                    </div>
                    <div class="flex flex-col">
                        <span class="text-lg font-bold bg-gradient-to-r from-lautech-700 to-teal-600 bg-clip-text text-transparent leading-tight">LAUMSA-SCOME</span>
                        <span class="text-xs text-slate-500 font-medium tracking-wider">LIBRARY</span>
                    </div>
                </div>
                
                <div class="hidden md:flex items-center space-x-8">
                    <button onclick="showSection('resources')" class="nav-link text-slate-600 hover:text-lautech-600 font-medium transition">Resources</button>
                    <button onclick="showSection('seniors')" class="nav-link text-slate-600 hover:text-lautech-600 font-medium transition">Seniors & Admins</button>
                    <button onclick="showSection('upload')" class="nav-link text-slate-600 hover:text-lautech-600 font-medium transition">Upload</button>
                    <button onclick="showSection('about')" class="nav-link text-slate-600 hover:text-lautech-600 font-medium transition">About</button>
                </div>

                <div class="flex items-center gap-4">
                    <div class="relative hidden sm:block">
                        <input type="text" id="globalSearch" placeholder="Search resources..." 
                            class="pl-10 pr-4 py-2 rounded-full border border-slate-300 focus:outline-none focus:ring-2 focus:ring-lautech-600 focus:border-transparent w-64 transition-all"
                            onkeyup="handleGlobalSearch(event)">
                        <i class="fas fa-search absolute left-3 top-3 text-slate-400"></i>
                    </div>
                    <button onclick="toggleMobileMenu()" class="md:hidden text-slate-600 hover:text-lautech-600">
                        <i class="fas fa-bars text-xl"></i>
                    </button>
                </div>
            </div>
        </div>
        
        <!-- Mobile Menu -->
        <div id="mobileMenu" class="hidden md:hidden bg-white border-t border-slate-200">
            <div class="px-4 pt-2 pb-4 space-y-2">
                <button onclick="showSection('resources')" class="block w-full text-left px-3 py-2 rounded-md text-slate-600 hover:bg-lautech-50">Resources</button>
                <button onclick="showSection('seniors')" class="block w-full text-left px-3 py-2 rounded-md text-slate-600 hover:bg-lautech-50">Seniors & Admins</button>
                <button onclick="showSection('upload')" class="block w-full text-left px-3 py-2 rounded-md text-slate-600 hover:bg-lautech-50">Upload</button>
            </div>
        </div>
    </nav>

    <!-- Hero Section -->
    <section id="home" class="section pt-24 pb-12 px-4 sm:px-6 lg:px-8 max-w-7xl mx-auto">
        <div class="text-center py-16 lg:py-24">
            <div class="inline-flex items-center gap-2 px-4 py-2 rounded-full bg-lautech-50 text-lautech-700 text-sm font-medium mb-6 animate-fade-in">
                <i class="fas fa-graduation-cap"></i>
                <span>LAUTECH Medical Students Association - SCOME</span>
            </div>
            <h1 class="text-4xl md:text-6xl font-bold text-slate-900 mb-6 leading-tight animate-fade-in">
                <span class="text-transparent bg-clip-text bg-gradient-to-r from-lautech-600 to-teal-500">LAUMSA-SCOME</span><br>
                <span class="text-3xl md:text-5xl">Medical Library</span>
            </h1>
            <p class="text-xl text-slate-600 mb-10 max-w-2xl mx-auto animate-fade-in">
                The official digital resource platform for Ladoke Akintola University of Technology Medical Students. Access textbooks, lecture notes, slides, and connect with senior mentors in Ogbomoso.
            </p>
            
            <div class="flex flex-col sm:flex-row gap-4 justify-center items-center animate-fade-in">
                <button onclick="showSection('resources')" class="px-8 py-4 bg-gradient-to-r from-lautech-600 to-lautech-700 text-white rounded-full font-semibold shadow-lg hover:shadow-xl transform hover:-translate-y-1 transition-all flex items-center gap-2">
                    <i class="fas fa-book-open"></i>
                    Browse Resources
                </button>
                <button onclick="showSection('seniors')" class="px-8 py-4 bg-white text-lautech-700 border-2 border-lautech-200 rounded-full font-semibold hover:bg-lautech-50 transition-all flex items-center gap-2">
                    <i class="fas fa-users"></i>
                    Connect with Seniors
                </button>
            </div>

            <!-- Stats -->
            <div class="grid grid-cols-2 md:grid-cols-4 gap-6 mt-16 max-w-4xl mx-auto">
                <div class="p-4 bg-white rounded-2xl shadow-sm border border-slate-100">
                    <div class="text-3xl font-bold text-lautech-600">500+</div>
                    <div class="text-sm text-slate-500 mt-1">Study Resources</div>
                </div>
                <div class="p-4 bg-white rounded-2xl shadow-sm border border-slate-100">
                    <div class="text-3xl font-bold text-teal-600">50+</div>
                    <div class="text-sm text-slate-500 mt-1">Senior Mentors</div>
                </div>
                <div class="p-4 bg-white rounded-2xl shadow-sm border border-slate-100">
                    <div class="text-3xl font-bold text-lautech-600">15</div>
                    <div class="text-sm text-slate-500 mt-1">Departments</div>
                </div>
                <div class="p-4 bg-white rounded-2xl shadow-sm border border-slate-100">
                    <div class="text-3xl font-bold text-teal-600">24/7</div>
                    <div class="text-sm text-slate-500 mt-1">Access</div>
                </div>
            </div>
        </div>
    </section>

    <!-- Resources Section -->
    <section id="resources" class="section hidden pt-24 pb-12 px-4 sm:px-6 lg:px-8 max-w-7xl mx-auto">
        <div class="flex flex-col md:flex-row justify-between items-start md:items-center mb-8 gap-4">
            <div>
                <h2 class="text-3xl font-bold text-slate-900">Study Resources</h2>
                <p class="text-slate-600 mt-1">Browse textbooks, notes, slides, and past papers from LAUTECH Medical School</p>
            </div>
            <div class="flex gap-2">
                <select id="sortSelect" onchange="sortResources()" class="px-4 py-2 rounded-lg border border-slate-300 focus:outline-none focus:ring-2 focus:ring-lautech-600">
                    <option value="newest">Newest First</option>
                    <option value="popular">Most Popular</option>
                    <option value="name">Name A-Z</option>
                </select>
                <button onclick="toggleView()" class="p-2 rounded-lg border border-slate-300 hover:bg-slate-50 transition">
                    <i id="viewIcon" class="fas fa-th-large text-slate-600"></i>
                </button>
            </div>
        </div>

        <!-- Category Pills -->
        <div class="flex flex-wrap gap-3 mb-8 overflow-x-auto pb-2">
            <button onclick="filterCategory('all')" class="category-pill active px-6 py-2 rounded-full bg-slate-200 text-slate-700 font-medium text-sm">All Resources</button>
            <button onclick="filterCategory('textbook')" class="category-pill px-6 py-2 rounded-full bg-slate-200 text-slate-700 font-medium text-sm">Textbooks</button>
            <button onclick="filterCategory('notes')" class="category-pill px-6 py-2 rounded-full bg-slate-200 text-slate-700 font-medium text-sm">Lecture Notes</button>
            <button onclick="filterCategory('slides')" class="category-pill px-6 py-2 rounded-full bg-slate-200 text-slate-700 font-medium text-sm">Slides/PPTs</button>
            <button onclick="filterCategory('pastpapers')" class="category-pill px-6 py-2 rounded-full bg-slate-200 text-slate-700 font-medium text-sm">Past Papers</button>
            <button onclick="filterCategory('anatomy')" class="category-pill px-6 py-2 rounded-full bg-slate-200 text-slate-700 font-medium text-sm">Anatomy</button>
            <button onclick="filterCategory('physiology')" class="category-pill px-6 py-2 rounded-full bg-slate-200 text-slate-700 font-medium text-sm">Physiology</button>
            <button onclick="filterCategory('pathology')" class="category-pill px-6 py-2 rounded-full bg-slate-200 text-slate-700 font-medium text-sm">Pathology</button>
        </div>

        <!-- Resources Grid -->
        <div id="resourcesGrid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
            <!-- Resource cards will be populated by JavaScript -->
        </div>

        <!-- Empty State -->
        <div id="emptyState" class="hidden text-center py-20">
            <div class="w-24 h-24 bg-slate-100 rounded-full flex items-center justify-center mx-auto mb-4">
                <i class="fas fa-search text-3xl text-slate-400"></i>
            </div>
            <h3 class="text-lg font-semibold text-slate-900">No resources found</h3>
            <p class="text-slate-600 mt-2">Try adjusting your search or category filter</p>
        </div>
    </section>

    <!-- Seniors & Admins Section -->
    <section id="seniors" class="section hidden pt-24 pb-12 px-4 sm:px-6 lg:px-8 max-w-7xl mx-auto">
        <div class="mb-8">
            <h2 class="text-3xl font-bold text-slate-900">Connect with Seniors & Admins</h2>
            <p class="text-slate-600 mt-1">Get guidance from experienced LAUMSA students and SCOME administrators at LAUTECH</p>
        </div>

        <!-- Tabs -->
        <div class="flex border-b border-slate-200 mb-8">
            <button onclick="switchTab('seniors')" id="tab-seniors" class="tab-active px-6 py-3 font-medium text-slate-700 hover:text-lautech-600 transition">
                <i class="fas fa-user-graduate mr-2"></i>LAUMSA Seniors
            </button>
            <button onclick="switchTab('admins')" id="tab-admins" class="px-6 py-3 font-medium text-slate-500 hover:text-lautech-600 transition">
                <i class="fas fa-user-shield mr-2"></i>SCOME Admins
            </button>
            <button onclick="switchTab('mentorship')" id="tab-mentorship" class="px-6 py-3 font-medium text-slate-500 hover:text-lautech-600 transition">
                <i class="fas fa-hands-helping mr-2"></i>Request Help
            </button>
        </div>

        <!-- Seniors Tab Content -->
        <div id="content-seniors" class="tab-content">
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6" id="seniorsGrid">
                <!-- Senior cards populated by JS -->
            </div>
        </div>

        <!-- Admins Tab Content -->
        <div id="content-admins" class="tab-content hidden">
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6" id="adminsGrid">
                <!-- Admin cards populated by JS -->
            </div>
        </div>

        <!-- Mentorship Request Form -->
        <div id="content-mentorship" class="tab-content hidden">
            <div class="max-w-2xl mx-auto bg-white rounded-2xl shadow-sm border border-slate-200 p-8">
                <h3 class="text-xl font-bold text-slate-900 mb-6">Request Academic Assistance</h3>
                <form onsubmit="submitHelpRequest(event)" class="space-y-6">
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <label class="block text-sm font-medium text-slate-700 mb-2">Your Name</label>
                            <input type="text" required class="w-full px-4 py-2 rounded-lg border border-slate-300 focus:outline-none focus:ring-2 focus:ring-lautech-600" placeholder="Full Name">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-slate-700 mb-2">Email / Phone</label>
                            <input type="text" required class="w-full px-4 py-2 rounded-lg border border-slate-300 focus:outline-none focus:ring-2 focus:ring-lautech-600" placeholder="Contact info">
                        </div>
                    </div>
                    
                    <div>
                        <label class="block text-sm font-medium text-slate-700 mb-2">Year of Study</label>
                        <select class="w-full px-4 py-2 rounded-lg border border-slate-300 focus:outline-none focus:ring-2 focus:ring-lautech-600">
                            <option>100 Level (Pre-clinical)</option>
                            <option>200 Level (Anatomy/Physiology)</option>
                            <option>300 Level (Pathology/Pharmacology)</option>
                            <option>400 Level (Clinical Rotations)</option>
                            <option>500 Level (Final Year)</option>
                            <option>600 Level (Internship)</option>
                        </select>
                    </div>

                    <div>
                        <label class="block text-sm font-medium text-slate-700 mb-2">Subject Area</label>
                        <select class="w-full px-4 py-2 rounded-lg border border-slate-300 focus:outline-none focus:ring-2 focus:ring-lautech-600">
                            <option>Anatomy</option>
                            <option>Physiology</option>
                            <option>Biochemistry</option>
                            <option>Pathology</option>
                            <option>Pharmacology</option>
                            <option>Microbiology</option>
                            <option>Forensic Medicine</option>
                            <option>Community Medicine</option>
                            <option>Medicine</option>
                            <option>Surgery</option>
                            <option>Paediatrics</option>
                            <option>Obstetrics & Gynaecology</option>
                        </select>
                    </div>

                    <div>
                        <label class="block text-sm font-medium text-slate-700 mb-2">Type of Help Needed</label>
                        <div class="grid grid-cols-2 gap-3">
                            <label class="flex items-center gap-2 p-3 border rounded-lg cursor-pointer hover:bg-slate-50">
                                <input type="checkbox" class="rounded text-lautech-600 focus:ring-lautech-600">
                                <span class="text-sm">Study Guidance</span>
                            </label>
                            <label class="flex items-center gap-2 p-3 border rounded-lg cursor-pointer hover:bg-slate-50">
                                <input type="checkbox" class="rounded text-lautech-600 focus:ring-lautech-600">
                                <span class="text-sm">Resource Location</span>
                            </label>
                            <label class="flex items-center gap-2 p-3 border rounded-lg cursor-pointer hover:bg-slate-50">
                                <input type="checkbox" class="rounded text-lautech-600 focus:ring-lautech-600">
                                <span class="text-sm">Exam Preparation</span>
                            </label>
                            <label class="flex items-center gap-2 p-3 border rounded-lg cursor-pointer hover:bg-slate-50">
                                <input type="checkbox" class="rounded text-lautech-600 focus:ring-lautech-600">
                                <span class="text-sm">Clinical Skills</span>
                            </label>
                        </div>
                    </div>

                    <div>
                        <label class="block text-sm font-medium text-slate-700 mb-2">Message</label>
                        <textarea rows="4" class="w-full px-4 py-2 rounded-lg border border-slate-300 focus:outline-none focus:ring-2 focus:ring-lautech-600" placeholder="Describe what help you need..."></textarea>
                    </div>

                    <button type="submit" class="w-full py-3 bg-gradient-to-r from-lautech-600 to-lautech-700 text-white rounded-lg font-semibold hover:shadow-lg transition-all">
                        <i class="fas fa-paper-plane mr-2"></i>Submit Request to SCOME
                    </button>
                </form>
            </div>
        </div>
    </section>

    <!-- Upload Section -->
    <section id="upload" class="section hidden pt-24 pb-12 px-4 sm:px-6 lg:px-8 max-w-4xl mx-auto">
        <div class="mb-8">
            <h2 class="text-3xl font-bold text-slate-900">Upload Resources</h2>
            <p class="text-slate-600 mt-1">Share your notes, slides, and study materials with LAUMSA fellow students at LAUTECH</p>
        </div>

        <div class="bg-white rounded-2xl shadow-sm border border-slate-200 p-8">
            <form onsubmit="handleUpload(event)" class="space-y-6">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div>
                        <label class="block text-sm font-medium text-slate-700 mb-2">Resource Title *</label>
                        <input type="text" id="uploadTitle" required class="w-full px-4 py-2 rounded-lg border border-slate-300 focus:outline-none focus:ring-2 focus:ring-lautech-600" placeholder="e.g., Cardiology Lecture Notes Chapter 3">
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-slate-700 mb-2">Category *</label>
                        <select id="uploadCategory" required class="w-full px-4 py-2 rounded-lg border border-slate-300 focus:outline-none focus:ring-2 focus:ring-lautech-600">
                            <option value="">Select Category</option>
                            <option value="textbook">Textbook/Reference</option>
                            <option value="notes">Lecture Notes</option>
                            <option value="slides">Slides/Presentation</option>
                            <option value="pastpapers">Past Papers (MB/BS)</option>
                            <option value="anatomy">Anatomy</option>
                            <option value="physiology">Physiology</option>
                            <option value="pathology">Pathology</option>
                            <option value="pharmacology">Pharmacology</option>
                            <option value="microbiology">Microbiology</option>
                            <option value="clinical">Clinical Medicine</option>
                            <option value="surgery">Surgery</option>
                            <option value="paediatrics">Paediatrics</option>
                            <option value="obgyn">Obstetrics & Gynaecology</option>
                        </select>
                    </div>
                </div>

                <div>
                    <label class="block text-sm font-medium text-slate-700 mb-2">Description</label>
                    <textarea id="uploadDesc" rows="3" class="w-full px-4 py-2 rounded-lg border border-slate-300 focus:outline-none focus:ring-2 focus:ring-lautech-600" placeholder="Brief description of the content..."></textarea>
                </div>

                <div>
                    <label class="block text-sm font-medium text-slate-700 mb-2">Upload File(s) *</label>
                    <div id="dropZone" class="upload-zone rounded-xl p-8 text-center cursor-pointer" onclick="document.getElementById('fileInput').click()" ondrop="dropHandler(event)" ondragover="dragOverHandler(event)" ondragleave="dragLeaveHandler(event)">
                        <input type="file" id="fileInput" class="hidden" multiple onchange="handleFileSelect(event)">
                        <div class="w-16 h-16 bg-lautech-50 rounded-full flex items-center justify-center mx-auto mb-4">
                            <i class="fas fa-cloud-upload-alt text-2xl text-lautech-600"></i>
                        </div>
                        <p class="text-slate-700 font-medium mb-1">Click to upload or drag and drop</p>
                        <p class="text-sm text-slate-500">PDF, PPT, DOCX up to 50MB</p>
                        <div id="selectedFiles" class="mt-4 space-y-2"></div>
                    </div>
                </div>

                <div class="flex items-start gap-3">
                    <input type="checkbox" id="terms" required class="mt-1 rounded text-lautech-600 focus:ring-lautech-600">
                    <label for="terms" class="text-sm text-slate-600">
                        I confirm this is my own work or I have permission to share it, and it doesn't contain copyrighted material. I agree to LAUMSA-SCOME content guidelines.
                    </label>
                </div>

                <div class="flex gap-4">
                    <button type="submit" class="flex-1 py-3 bg-gradient-to-r from-lautech-600 to-lautech-700 text-white rounded-lg font-semibold hover:shadow-lg transition-all">
                        <i class="fas fa-upload mr-2"></i>Upload to LAUMSA Library
                    </button>
                    <button type="button" onclick="resetUpload()" class="px-6 py-3 border border-slate-300 rounded-lg font-medium text-slate-700 hover:bg-slate-50 transition">
                        Reset
                    </button>
                </div>
            </form>
        </div>

        <!-- Upload Guidelines -->
        <div class="mt-8 bg-teal-50 rounded-xl p-6 border border-teal-100">
            <h4 class="font-semibold text-teal-900 mb-3"><i class="fas fa-info-circle mr-2"></i>LAUMSA-SCOME Upload Guidelines</h4>
            <ul class="space-y-2 text-sm text-teal-800">
                <li class="flex items-start gap-2"><i class="fas fa-check mt-1"></i> Only upload materials you have created or have explicit permission to share</li>
                <li class="flex items-start gap-2"><i class="fas fa-check mt-1"></i> Ensure files are properly named and organized (CourseCode_Topic_Type)</li>
                <li class="flex items-start gap-2"><i class="fas fa-check mt-1"></i> Scanned notes should be legible and properly rotated</li>
                <li class="flex items-start gap-2"><i class="fas fa-check mt-1"></i> SCOME admins will review uploads within 24-48 hours before publishing</li>
                <li class="flex items-start gap-2"><i class="fas fa-check mt-1"></i> Include your LAUTECH student ID for verification</li>
                <li class="flex items-start gap-2"><i class="fas fa-check mt-1"></i> MB/BS past papers should follow NIMSA guidelines</li>
            </ul>
        </div>
    </section>

    <!-- About Section -->
    <section id="about" class="section hidden pt-24 pb-12 px-4 sm:px-6 lg:px-8 max-w-4xl mx-auto">
        <div class="bg-white rounded-2xl shadow-sm border border-slate-200 p-8 md:p-12">
            <div class="text-center mb-8">
                <div class="w-20 h-20 bg-gradient-to-br from-lautech-600 to-teal-500 rounded-2xl flex items-center justify-center text-white text-3xl mx-auto mb-4 shadow-lg">
                    <i class="fas fa-book-medical"></i>
                </div>
                <h2 class="text-3xl font-bold text-slate-900">About LAUMSA-SCOME Library</h2>
                <p class="text-lautech-600 font-medium mt-2">Ladoke Akintola University of Technology, Ogbomoso</p>
            </div>
            
            <div class="prose prose-slate max-w-none">
                <p class="text-slate-600 mb-6 leading-relaxed">
                    The LAUMSA-SCOME Library is the official digital resource platform of the Ladoke Akintola University of Technology Medical Students Association (LAUMSA) Standing Committee on Medical Education (SCOME). This platform serves as a centralized hub for LAUTECH medical students to access study materials, share resources, and connect with senior mentors for academic guidance in Ogbomoso, Nigeria.
                </p>
                
                <div class="grid md:grid-cols-3 gap-6 my-8">
                    <div class="text-center p-4">
                        <div class="w-12 h-12 bg-lautech-50 rounded-full flex items-center justify-center mx-auto mb-3 text-lautech-600">
                            <i class="fas fa-book"></i>
                        </div>
                        <h4 class="font-semibold text-slate-900 mb-2">Centralized Resources</h4>
                        <p class="text-sm text-slate-600">All LAUTECH medical study materials organized by subject and type</p>
                    </div>
                    <div class="text-center p-4">
                        <div class="w-12 h-12 bg-teal-100 rounded-full flex items-center justify-center mx-auto mb-3 text-teal-600">
                            <i class="fas fa-network-wired"></i>
                        </div>
                        <h4 class="font-semibold text-slate-900 mb-2">Peer Support</h4>
                        <p class="text-sm text-slate-600">Connect with LAUMSA seniors for guidance and mentorship</p>
                    </div>
                    <div class="text-center p-4">
                        <div class="w-12 h-12 bg-lautech-50 rounded-full flex items-center justify-center mx-auto mb-3 text-lautech-600">
                            <i class="fas fa-sync"></i>
                        </div>
                        <h4 class="font-semibold text-slate-900 mb-2">NIMSA Aligned</h4>
                        <p class="text-sm text-slate-600">Resources aligned with Nigerian Medical Students Association standards</p>
                    </div>
                </div>

                <div class="bg-slate-50 rounded-xl p-6 mt-8">
                    <h3 class="font-bold text-slate-900 mb-4">Contact LAUMSA-SCOME Administration</h3>
                    <div class="space-y-3 text-slate-600">
                        <p class="flex items-center gap-3"><i class="fas fa-envelope text-lautech-600 w-5"></i> scome@laumsa.lautech.edu.ng</p>
                        <p class="flex items-center gap-3"><i class="fas fa-envelope text-lautech-600 w-5"></i> library@laumsa.lautech.edu.ng</p>
                        <p class="flex items-center gap-3"><i class="fas fa-phone text-lautech-600 w-5"></i> +234 806 XXX XXXX</p>
                        <p class="flex items-center gap-3"><i class="fas fa-map-marker-alt text-lautech-600 w-5"></i> LAUTECH College of Health Sciences, Ogbomoso, Oyo State, Nigeria</p>
                        <p class="flex items-center gap-3"><i class="fas fa-clock text-lautech-600 w-5"></i> Mon-Fri: 8:00 AM - 6:00 PM (WAT)</p>
                    </div>
                </div>

                <div class="mt-8 pt-8 border-t border-slate-200">
                    <p class="text-sm text-slate-500 text-center">
                        © 2026 LAUMSA-SCOME Library. Managed by the Standing Committee on Medical Education.<br>
                        Ladoke Akintola University of Technology Medical Students Association.<br>
                        A member of Nigerian Medical Students Association (NIMSA) South-West Region.
                    </p>
                </div>
            </div>
        </div>
    </section>

    <!-- Toast Notification -->
    <div id="toast" class="fixed bottom-4 right-4 bg-slate-800 text-white px-6 py-3 rounded-lg shadow-lg transform translate-y-20 opacity-0 transition-all duration-300 z-50 flex items-center gap-3">
        <i id="toastIcon" class="fas fa-check-circle text-green-400"></i>
        <span id="toastMessage">Operation successful</span>
    </div>

    <script>
        // Sample Data - LAUTECH Medical School Structure
        const resources = [
            { id: 1, title: "Gray's Anatomy for Students (Nigerian Edition)", category: "textbook", type: "PDF", size: "45 MB", author: "Dr. Drake et al.", downloads: 1234, date: "2024-01-15", icon: "fa-book" },
            { id: 2, title: "LAUTECH Cardiovascular System Lecture Notes", category: "notes", type: "PDF", size: "12 MB", author: "Dr. Adeyemi (Anatomy)", downloads: 892, date: "2024-02-20", icon: "fa-file-alt" },
            { id: 3, title: "Histology Practical Slides - Epithelial Tissue", category: "slides", type: "PPT", size: "28 MB", author: "Prof. Olatunji", downloads: 567, date: "2024-03-01", icon: "fa-file-powerpoint" },
            { id: 4, title: "MBBS Part I Past Questions (2020-2023)", category: "pastpapers", type: "PDF", size: "8 MB", author: "LAUMSA Academic Committee", downloads: 2341, date: "2023-12-10", icon: "fa-file-pdf" },
            { id: 5, title: "Neuroanatomy Atlas for Medical Students", category: "anatomy", type: "PDF", size: "65 MB", author: "Dr. Emeka Okafor", downloads: 1567, date: "2024-01-28", icon: "fa-brain" },
            { id: 6, title: "Renal Physiology Complete Notes (LAUTECH)", category: "physiology", type: "DOCX", size: "5 MB", author: "James Adewale", downloads: 445, date: "2024-03-15", icon: "fa-kidney" },
            { id: 7, title: "General Pathology Lecture Slides", category: "pathology", type: "PPT", size: "42 MB", author: "Dr. Fatima Abdullahi", downloads: 778, date: "2024-02-14", icon: "fa-microscope" },
            { id: 8, title: "Clinical Medicine Handbook - LAUTECH", category: "clinical", type: "PDF", size: "15 MB", author: "LAUTECH College of Health Sciences", downloads: 3122, date: "2024-01-05", icon: "fa-user-md" },
            { id: 9, title: "Pharmacology Drug Charts (Nigerian Market)", category: "pharmacology", type: "PDF", size: "3 MB", author: "Pharm. Chioma Nwosu", downloads: 2234, date: "2024-03-10", icon: "fa-pills" }
        ];

        const seniors = [
            { name: "Dr. Oluwaseun Adeleke", year: "600 Level (Final)", specialty: "Internal Medicine", rating: 4.9, reviews: 45, availability: "Available", image: "https://i.pravatar.cc/150?img=11", email: "adeleke.o@lautech.edu.ng", phone: "+234 806 123 4567" },
            { name: "Amina Ibrahim", year: "500 Level", specialty: "Surgery", rating: 4.8, reviews: 32, availability: "Busy", image: "https://i.pravatar.cc/150?img=5", email: "ibrahim.a@lautech.edu.ng", phone: "+234 806 234 5678" },
            { name: "Chukwuemeka Okafor", year: "500 Level", specialty: "Paediatrics", rating: 4.9, reviews: 28, availability: "Available", image: "https://i.pravatar.cc/150?img=3", email: "okafor.c@lautech.edu.ng", phone: "+234 806 345 6789" },
            { name: "Fatima Abdullahi", year: "600 Level (Final)", specialty: "Obstetrics & Gynae", rating: 4.7, reviews: 56, availability: "Available", image: "https://i.pravatar.cc/150?img=9", email: "abdullahi.f@lautech.edu.ng", phone: "+234 806 456 7890" },
            { name: "Olumide Adeyemi", year: "400 Level", specialty: "Psychiatry", rating: 4.6, reviews: 19, availability: "Limited", image: "https://i.pravatar.cc/150?img=12", email: "adeyemi.o@lautech.edu.ng", phone: "+234 806 567 8901" },
            { name: "Ngozi Eze", year: "600 Level (Final)", specialty: "Emergency Medicine", rating: 5.0, reviews: 41, availability: "Available", image: "https://i.pravatar.cc/150?img=10", email: "eze.n@lautech.edu.ng", phone: "+234 806 678 9012" }
        ];

        const admins = [
            { name: "Dr. Olatunde Ajayi", role: "SCOME President", department: "LAUMSA-SCOME", email: "president@laumsa.lautech.edu.ng", phone: "+234 803 XXX XXXX", office: "LAUTECH College of Health Sciences, SCOME Office", hours: "Mon-Fri: 9AM-5PM (WAT)", image: "https://i.pravatar.cc/150?img=1" },
            { name: "Prof. Grace Oluwatosin", role: "Academic Coordinator", department: "Medical Education", email: "academic@laumsa.lautech.edu.ng", phone: "+234 805 XXX XXXX", office: "LAUTECH CHS, Academic Affairs", hours: "Mon-Wed: 10AM-4PM", image: "https://i.pravatar.cc/150?img=8" },
            { name: "Emmanuel Nwachukwu", role: "IT & Library Lead", department: "Digital Resources", email: "it.library@laumsa.lautech.edu.ng", phone: "+234 807 XXX XXXX", office: "LAUTECH CHS, E-Library", hours: "Mon-Sat: 8AM-8PM", image: "https://i.pravatar.cc/150?img=6" },
            { name: "Adebola Ogunleye", role: "Content Curator", department: "SCOME Resources", email: "content@laumsa.lautech.edu.ng", phone: "+234 802 XXX XXXX", office: "LAUTECH CHS, Library Unit", hours: "Tue-Sat: 8AM-6PM", image: "https://i.pravatar.cc/150?img=13" }
        ];

        let currentCategory = 'all';
        let currentView = 'grid';

        // Initialize
        document.addEventListener('DOMContentLoaded', () => {
            renderResources();
            renderSeniors();
            renderAdmins();
        });

        // Navigation Functions
        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.section').forEach(section => {
                section.classList.add('hidden');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.remove('hidden');
            
            // Update nav active states
            document.querySelectorAll('.nav-link').forEach(link => {
                link.classList.remove('text-lautech-600');
                link.classList.add('text-slate-600');
            });
            
            // Close mobile menu if open
            document.getElementById('mobileMenu').classList.add('hidden');
            
            // Scroll to top
            window.scrollTo(0, 0);
        }

        function toggleMobileMenu() {
            const menu = document.getElementById('mobileMenu');
            menu.classList.toggle('hidden');
        }

        // Resource Functions
        function renderResources() {
            const grid = document.getElementById('resourcesGrid');
            const emptyState = document.getElementById('emptyState');
            
            let filtered = resources;
            if (currentCategory !== 'all') {
                filtered = resources.filter(r => r.category === currentCategory);
            }
            
            // Apply search filter if exists
            const searchTerm = document.getElementById('globalSearch').value.toLowerCase();
            if (searchTerm) {
                filtered = filtered.filter(r => r.title.toLowerCase().includes(searchTerm) || 
                                                r.author.toLowerCase().includes(searchTerm));
            }

            if (filtered.length === 0) {
                grid.innerHTML = '';
                emptyState.classList.remove('hidden');
                return;
            }
            
            emptyState.classList.add('hidden');
            
            grid.innerHTML = filtered.map(resource => `
                <div class="resource-card bg-white rounded-xl border border-slate-200 overflow-hidden hover:border-lautech-300">
                    <div class="p-6">
                        <div class="flex items-start justify-between mb-4">
                            <div class="w-12 h-12 bg-gradient-to-br from-lautech-50 to-teal-50 rounded-lg flex items-center justify-center text-lautech-600 text-xl">
                                <i class="fas ${resource.icon}"></i>
                            </div>
                            <span class="px-3 py-1 bg-slate-100 text-slate-600 text-xs font-medium rounded-full uppercase">${resource.type}</span>
                        </div>
                        
                        <h3 class="font-bold text-slate-900 mb-2 line-clamp-2" title="${resource.title}">${resource.title}</h3>
                        <p class="text-sm text-slate-500 mb-4">by ${resource.author}</p>
                        
                        <div class="flex items-center gap-4 text-xs text-slate-500 mb-4">
                            <span class="flex items-center gap-1"><i class="fas fa-download"></i> ${resource.downloads}</span>
                            <span class="flex items-center gap-1"><i class="fas fa-weight-hanging"></i> ${resource.size}</span>
                            <span class="flex items-center gap-1"><i class="fas fa-calendar"></i> ${resource.date}</span>
                        </div>
                        
                        <div class="flex gap-2">
                            <button onclick="downloadResource(${resource.id})" class="flex-1 py-2 bg-lautech-600 text-white rounded-lg text-sm font-medium hover:bg-lautech-700 transition flex items-center justify-center gap-2">
                                <i class="fas fa-download"></i> Download
                            </button>
                            <button onclick="previewResource(${resource.id})" class="px-3 py-2 border border-slate-300 rounded-lg text-slate-600 hover:bg-slate-50 transition">
                                <i class="fas fa-eye"></i>
                            </button>
                        </div>
                    </div>
                    <div class="px-6 py-3 bg-slate-50 border-t border-slate-100 flex items-center justify-between">
                        <span class="text-xs font-medium text-slate-500 capitalize">${resource.category}</span>
                        <button onclick="showContactForResource('${resource.author}')" class="text-xs text-lautech-600 hover:text-lautech-700 font-medium">
                            Contact Uploader
                        </button>
                    </div>
                </div>
            `).join('');
        }

        function filterCategory(category) {
            currentCategory = category;
            
            // Update pill styles
            document.querySelectorAll('.category-pill').forEach(pill => {
                pill.classList.remove('active');
            });
            event.target.classList.add('active');
            
            renderResources();
        }

        function handleGlobalSearch(e) {
            if (e.key === 'Enter') {
                showSection('resources');
            }
            renderResources();
        }

        function sortResources() {
            const sortType = document.getElementById('sortSelect').value;
            
            if (sortType === 'newest') {
                resources.sort((a, b) => new Date(b.date) - new Date(a.date));
            } else if (sortType === 'popular') {
                resources.sort((a, b) => b.downloads - a.downloads);
            } else if (sortType === 'name') {
                resources.sort((a, b) => a.title.localeCompare(b.title));
            }
            
            renderResources();
        }

        function toggleView() {
            const grid = document.getElementById('resourcesGrid');
            const icon = document.getElementById('viewIcon');
            
            if (currentView === 'grid') {
                currentView = 'list';
                grid.classList.remove('grid-cols-1', 'md:grid-cols-2', 'lg:grid-cols-3');
                grid.classList.add('grid-cols-1');
                icon.classList.remove('fa-th-large');
                icon.classList.add('fa-list');
            } else {
                currentView = 'grid';
                grid.classList.remove('grid-cols-1');
                grid.classList.add('grid-cols-1', 'md:grid-cols-2', 'lg:grid-cols-3');
                icon.classList.remove('fa-list');
                icon.classList.add('fa-th-large');
            }
        }

        function downloadResource(id) {
            const resource = resources.find(r => r.id === id);
            showToast(`Downloading ${resource.title}...`, 'fa-download');
            
            // Simulate download
            setTimeout(() => {
                resource.downloads++;
                renderResources();
                showToast('Download completed!', 'fa-check-circle');
            }, 1500);
        }

        function previewResource(id) {
            const resource = resources.find(r => r.id === id);
            showToast(`Opening preview for ${resource.title}`, 'fa-eye');
        }

        function showContactForResource(author) {
            showSection('seniors');
            showToast(`Contact information for ${author} available in Seniors tab`, 'fa-info-circle');
        }

        // Seniors & Admins Functions
        function renderSeniors() {
            const grid = document.getElementById('seniorsGrid');
            grid.innerHTML = seniors.map(senior => `
                <div class="senior-card bg-white rounded-xl border border-slate-200 p-6 hover:shadow-lg">
                    <div class="flex items-start gap-4 mb-4">
                        <img src="${senior.image}" alt="${senior.name}" class="w-16 h-16 rounded-full object-cover border-2 border-lautech-100">
                        <div class="flex-1">
                            <h3 class="font-bold text-slate-900">${senior.name}</h3>
                            <p class="text-sm text-lautech-600 font-medium">${senior.year} • ${senior.specialty}</p>
                            <div class="flex items-center gap-1 mt-1">
                                <i class="fas fa-star text-yellow-400 text-xs"></i>
                                <span class="text-sm font-medium text-slate-700">${senior.rating}</span>
                                <span class="text-xs text-slate-500">(${senior.reviews} reviews)</span>
                            </div>
                        </div>
                        <span class="px-2 py-1 rounded-full text-xs font-medium ${senior.availability === 'Available' ? 'bg-green-100 text-green-700' : senior.availability === 'Busy' ? 'bg-red-100 text-red-700' : 'bg-yellow-100 text-yellow-700'}">
                            ${senior.availability}
                        </span>
                    </div>
                    
                    <div class="space-y-2 mb-4 text-sm text-slate-600">
                        <p class="flex items-center gap-2"><i class="fas fa-envelope text-slate-400 w-4"></i> ${senior.email}</p>
                        <p class="flex items-center gap-2"><i class="fas fa-phone text-slate-400 w-4"></i> ${senior.phone}</p>
                    </div>
                    
                    <div class="flex gap-2">
                        <button onclick="contactSenior('${senior.email}')" class="flex-1 py-2 bg-lautech-600 text-white rounded-lg text-sm font-medium hover:bg-lautech-700 transition">
                            <i class="fas fa-envelope mr-1"></i> Email
                        </button>
                        <button onclick="callSenior('${senior.phone}')" class="flex-1 py-2 border border-lautech-600 text-lautech-600 rounded-lg text-sm font-medium hover:bg-lautech-50 transition">
                            <i class="fas fa-phone mr-1"></i> Call
                        </button>
                    </div>
                </div>
            `).join('');
        }

        function renderAdmins() {
            const grid = document.getElementById('adminsGrid');
            grid.innerHTML = admins.map(admin => `
                <div class="senior-card bg-white rounded-xl border border-slate-200 p-6 hover:shadow-lg">
                    <div class="flex items-start gap-4">
                        <img src="${admin.image}" alt="${admin.name}" class="w-20 h-20 rounded-full object-cover border-2 border-teal-100">
                        <div class="flex-1">
                            <h3 class="font-bold text-slate-900 text-lg">${admin.name}</h3>
                            <p class="text-teal-600 font-medium">${admin.role}</p>
                            <p class="text-sm text-slate-500">${admin.department}</p>
                            
                            <div class="mt-4 space-y-2 text-sm text-slate-600">
                                <p class="flex items-center gap-2"><i class="fas fa-envelope text-slate-400 w-4"></i> ${admin.email}</p>
                                <p class="flex items-center gap-2"><i class="fas fa-phone text-slate-400 w-4"></i> ${admin.phone}</p>
                                <p class="flex items-center gap-2"><i class="fas fa-door-open text-slate-400 w-4"></i> ${admin.office}</p>
                                <p class="flex items-center gap-2"><i class="fas fa-clock text-slate-400 w-4"></i> ${admin.hours}</p>
                            </div>
                            
                            <div class="mt-4 flex gap-2">
                                <button onclick="contactSenior('${admin.email}')" class="px-4 py-2 bg-teal-600 text-white rounded-lg text-sm font-medium hover:bg-teal-700 transition">
                                    <i class="fas fa-envelope mr-1"></i> Contact
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            `).join('');
        }

        function switchTab(tab) {
            // Update tab styles
            document.querySelectorAll('[id^="tab-"]').forEach(t => {
                t.classList.remove('tab-active');
                t.classList.add('text-slate-500');
            });
            document.getElementById(`tab-${tab}`).classList.add('tab-active');
            document.getElementById(`tab-${tab}`).classList.remove('text-slate-500');
            
            // Show/hide content
            document.querySelectorAll('.tab-content').forEach(content => {
                content.classList.add('hidden');
            });
            document.getElementById(`content-${tab}`).classList.remove('hidden');
        }

        function contactSenior(email) {
            window.location.href = `mailto:${email}`;
            showToast(`Opening email to ${email}`, 'fa-envelope');
        }

        function callSenior(phone) {
            window.location.href = `tel:${phone}`;
            showToast(`Dialing ${phone}`, 'fa-phone');
        }

        function submitHelpRequest(e) {
            e.preventDefault();
            showToast('Help request submitted to SCOME! A senior will contact you soon.', 'fa-check-circle');
            e.target.reset();
        }

        // Upload Functions
        function dragOverHandler(e) {
            e.preventDefault();
            e.currentTarget.classList.add('dragover');
        }

        function dragLeaveHandler(e) {
            e.currentTarget.classList.remove('dragover');
        }

        function dropHandler(e) {
            e.preventDefault();
            e.currentTarget.classList.remove('dragover');
            const files = e.dataTransfer.files;
            handleFiles(files);
        }

        function handleFileSelect(e) {
            const files = e.target.files;
            handleFiles(files);
        }

        function handleFiles(files) {
            const container = document.getElementById('selectedFiles');
            container.innerHTML = '';
            
            Array.from(files).forEach(file => {
                const div = document.createElement('div');
                div.className = 'flex items-center justify-between p-3 bg-slate-50 rounded-lg border border-slate-200';
                div.innerHTML = `
                    <div class="flex items-center gap-3">
                        <i class="fas fa-file text-lautech-600"></i>
                        <span class="text-sm font-medium text-slate-700">${file.name}</span>
                        <span class="text-xs text-slate-500">(${(file.size / 1024 / 1024).toFixed(2)} MB)</span>
                    </div>
                    <button onclick="this.parentElement.remove()" class="text-red-500 hover:text-red-700">
                        <i class="fas fa-times"></i>
                    </button>
                `;
                container.appendChild(div);
            });
        }

        function handleUpload(e) {
            e.preventDefault();
            
            const title = document.getElementById('uploadTitle').value;
            const category = document.getElementById('uploadCategory').value;
            
            // Simulate upload
            showToast('Uploading resource to LAUMSA Library...', 'fa-upload');
            
            setTimeout(() => {
                // Add to resources
                const newResource = {
                    id: resources.length + 1,
                    title: title,
                    category: category,
                    type: "PDF",
                    size: "2.5 MB",
                    author: "LAUMSA Student",
                    downloads: 0,
                    date: new Date().toISOString().split('T')[0],
                    icon: "fa-file-alt"
                };
                
                resources.unshift(newResource);
                showToast('Resource uploaded successfully! Pending SCOME approval.', 'fa-check-circle');
                resetUpload();
            }, 2000);
        }

        function resetUpload() {
            document.getElementById('uploadTitle').value = '';
            document.getElementById('uploadCategory').value = '';
            document.getElementById('uploadDesc').value = '';
            document.getElementById('fileInput').value = '';
            document.getElementById('selectedFiles').innerHTML = '';
            document.getElementById('terms').checked = false;
        }

        // Toast Notification
        function showToast(message, icon = 'fa-check-circle') {
            const toast = document.getElementById('toast');
            const toastIcon = document.getElementById('toastIcon');
            const toastMessage = document.getElementById('toastMessage');
            
            toastIcon.className = `fas ${icon} text-green-400`;
            toastMessage.textContent = message;
            
            toast.classList.remove('translate-y-20', 'opacity-0');
            
            setTimeout(() => {
                toast.classList.add('translate-y-20', 'opacity-0');
            }, 3000);
        }

        // Close mobile menu when clicking outside
        document.addEventListener('click', (e) => {
            const menu = document.getElementById('mobileMenu');
            const button = e.target.closest('button');
            if (!button || !button.onclick || !button.onclick.toString().includes('toggleMobileMenu')) {
                if (!e.target.closest('#mobileMenu')) {
                    menu.classList.add('hidden');
                }
            }
        });
    </script>
</body>
</html>
