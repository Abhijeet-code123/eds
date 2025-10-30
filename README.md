<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Echelon Dev Society (EDS)</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800&family=Space+Grotesk:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary: #007bff;
            --primary-dark: #0056b3;
            --primary-light: #66b3ff;
            --background: #ffffff;
            --foreground: #1f2937;
            --card: #f9fafb;
            --border: #e5e7eb;
            --muted: #6b7280;
        }

        [data-theme="dark"] {
            --background: #0f1419;
            --foreground: #f3f4f6;
            --card: #1a1f29;
            --border: #374151;
            --muted: #9ca3af;
        }

        html {
            scroll-behavior: smooth;
        }

        body {
            font-family: 'Poppins', sans-serif;
            background: var(--background);
            color: var(--foreground);
            overflow-x: hidden;
            transition: background-color 0.3s ease, color 0.3s ease;
        }

        /* Animations */
        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-20px); }
        }

        @keyframes fadeInUp {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes bounce-slow {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }

        @keyframes shimmer {
            0% { background-position: -1000px 0; }
            100% { background-position: 1000px 0; }
        }

        @keyframes pulse-glow {
            0%, 100% { box-shadow: 0 0 20px rgba(0, 123, 255, 0.4), 0 0 40px rgba(0, 123, 255, 0.2); }
            50% { box-shadow: 0 0 30px rgba(0, 123, 255, 0.6), 0 0 60px rgba(0, 123, 255, 0.3); }
        }

        @keyframes pattern-move {
            from { background-position: 0 0, 0 0, 0 0; }
            to { background-position: 100px 100px, 60px 60px, 60px 60px; }
        }

        /* Navigation */
        nav {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            z-index: 1000;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-bottom: 1px solid var(--border);
            transition: all 0.3s ease;
        }

        [data-theme="dark"] nav {
            background: rgba(15, 20, 25, 0.95);
        }

        .nav-container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 1rem 1.5rem;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .logo-section {
            display: flex;
            align-items: center;
            gap: 0.75rem;
        }

        .logo-img {
            width: 44px;
            height: 44px;
            animation: pulse-glow 2s ease-in-out infinite;
            border-radius: 0.5rem;
        }

        .logo-text {
            font-family: 'Space Grotesk', sans-serif;
            font-size: 1.5rem;
            font-weight: 700;
            background: linear-gradient(135deg, var(--primary), var(--primary-dark));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .nav-links {
            display: flex;
            gap: 2rem;
            list-style: none;
        }

        .nav-links a {
            position: relative;
            text-decoration: none;
            color: var(--foreground);
            font-weight: 500;
            transition: color 0.3s;
        }

        .nav-links a::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 0;
            height: 2px;
            background: var(--primary);
            transition: width 0.3s;
        }

        .nav-links a:hover::after {
            width: 100%;
        }

        .nav-right {
            display: flex;
            align-items: center;
            gap: 2rem;
        }

        .theme-toggle {
            width: 48px;
            height: 28px;
            border-radius: 50px;
            border: 2px solid var(--primary);
            background: var(--card);
            cursor: pointer;
            position: relative;
            transition: background-color 0.3s;
        }

        .theme-toggle-slider {
            position: absolute;
            top: 2px;
            left: 2px;
            width: 20px;
            height: 20px;
            border-radius: 50%;
            background: var(--primary);
            transition: left 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 10px;
        }

        [data-theme="dark"] .theme-toggle-slider {
            left: 22px;
        }

        .burger {
            display: none;
            flex-direction: column;
            gap: 5px;
            cursor: pointer;
            padding: 0.5rem;
        }

        .burger span {
            width: 25px;
            height: 3px;
            background: var(--foreground);
            transition: 0.3s;
        }

        /* Hero Section */
        .hero {
            position: relative;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
            padding: 2rem 1.5rem;
        }

        .pattern-bg {
            position: absolute;
            inset: 0;
            opacity: 0.7;
            animation: pattern-move 120s linear infinite;
            background-image: 
                radial-gradient(circle at 25px 25px, rgba(0, 123, 255, 0.08) 2px, transparent 3px),
                linear-gradient(45deg, transparent 49%, rgba(0, 123, 255, 0.05) 50%, transparent 51%),
                linear-gradient(-45deg, transparent 49%, rgba(0, 123, 255, 0.05) 50%, transparent 51%);
            background-size: 50px 50px, 30px 30px, 30px 30px;
        }

        [data-theme="dark"] .pattern-bg {
            opacity: 0.5;
        }

        .hero-gradient {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            height: 10rem;
            background: linear-gradient(to top, var(--background), transparent);
            z-index: 10;
        }

        .hero-content {
            position: relative;
            z-index: 20;
            max-width: 900px;
            text-align: center;
        }

        .hero-logo {
            width: 280px;
            height: 280px;
            margin: 0 auto 2rem;
            animation: float 3s ease-in-out infinite;
            filter: drop-shadow(0 20px 40px rgba(0, 123, 255, 0.4));
        }

        .hero h1 {
            font-family: 'Space Grotesk', sans-serif;
            font-size: 4rem;
            font-weight: 700;
            margin-bottom: 1.5rem;
            background: linear-gradient(135deg, var(--primary), var(--primary-dark));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            animation: fadeInUp 1s ease;
        }

        .hero p {
            font-size: 1.3rem;
            margin-bottom: 2rem;
            color: var(--muted);
            animation: fadeInUp 1s ease 0.2s backwards;
        }

        .cta-button {
            display: inline-block;
            padding: 1rem 3rem;
            background: linear-gradient(135deg, var(--primary), var(--primary-dark));
            color: white;
            text-decoration: none;
            border: none;
            border-radius: 50px;
            font-weight: 600;
            font-size: 1.1rem;
            cursor: pointer;
            transition: transform 0.3s, box-shadow 0.3s;
            animation: fadeInUp 1s ease 0.4s backwards;
            box-shadow: 0 10px 30px rgba(0, 123, 255, 0.3);
        }

        .cta-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 40px rgba(0, 123, 255, 0.5);
        }

        .scroll-indicator {
            position: absolute;
            bottom: 2rem;
            left: 50%;
            transform: translateX(-50%);
            z-index: 20;
            animation: bounce-slow 2s ease-in-out infinite;
            color: var(--primary);
            cursor: pointer;
        }

        /* Sections */
        section {
            padding: 6rem 1.5rem;
            max-width: 1400px;
            margin: 0 auto;
        }

        .section-title {
            font-family: 'Space Grotesk', sans-serif;
            font-size: 3rem;
            font-weight: 700;
            text-align: center;
            margin-bottom: 3rem;
            position: relative;
        }

        .section-title span {
            background: linear-gradient(135deg, var(--primary), var(--primary-dark));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .section-title::after {
            content: '';
            position: absolute;
            bottom: -0.5rem;
            left: 50%;
            transform: translateX(-50%);
            width: 80px;
            height: 4px;
            background: linear-gradient(135deg, var(--primary), var(--primary-dark));
            border-radius: 2px;
        }

        /* About Section */
        .about-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 4rem;
            align-items: center;
        }

        .about-text h3 {
            font-size: 2rem;
            color: var(--primary);
            margin-bottom: 1rem;
        }

        .about-text p {
            font-size: 1.1rem;
            line-height: 1.8;
            margin-bottom: 1.5rem;
            color: var(--foreground);
            opacity: 0.9;
        }

        .about-image {
            height: 400px;
            border-radius: 1.5rem;
            background: linear-gradient(135deg, rgba(0, 123, 255, 0.2), rgba(0, 86, 179, 0.2)),
                        url('https://images.unsplash.com/photo-1522071820081-009f0129c71c?w=800&q=80') center/cover;
            transition: transform 0.3s;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.1);
        }

        .about-image:hover {
            transform: scale(1.02);
        }

        /* Team Section */
        #team {
            background: var(--card);
        }

        .team-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 2rem;
        }

        .team-card {
            position: relative;
            background: var(--card);
            backdrop-filter: blur(10px);
            border-radius: 1.5rem;
            padding: 2rem;
            text-align: center;
            transition: transform 0.3s, box-shadow 0.3s;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.08);
        }

        .team-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 4px;
            background: linear-gradient(90deg, var(--primary), var(--primary-dark));
            transform: scaleX(0);
            transition: transform 0.3s;
        }

        .team-card:hover::before {
            transform: scaleX(1);
        }

        .team-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 50px rgba(0, 123, 255, 0.2);
        }

        .team-photo {
            width: 140px;
            height: 140px;
            margin: 0 auto 1.5rem;
            padding: 1.25rem;
            background: white;
            border-radius: 50%;
            box-shadow: 0 10px 30px rgba(0, 123, 255, 0.3);
            transition: transform 0.3s;
        }

        .team-card:hover .team-photo {
            transform: scale(1.1);
        }

        .team-photo img {
            width: 100%;
            height: 100%;
            object-fit: contain;
        }

        .team-card h3 {
            font-size: 1.3rem;
            margin-bottom: 0.5rem;
        }

        .team-card p {
            color: var(--primary);
            font-weight: 600;
        }

        /* Events Section */
        .events-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
        }

        .event-card {
            background: var(--card);
            backdrop-filter: blur(10px);
            border-radius: 1.5rem;
            overflow: hidden;
            transition: transform 0.3s, box-shadow 0.3s;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.08);
        }

        .event-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 60px rgba(0, 123, 255, 0.3);
        }

        .event-image {
            height: 200px;
            background-size: cover;
            background-position: center;
            transition: transform 0.5s;
        }

        .event-card:hover .event-image {
            transform: scale(1.1);
        }

        .event-content {
            padding: 1.5rem;
        }

        .event-content h3 {
            font-size: 1.5rem;
            margin-bottom: 0.75rem;
        }

        .event-content p {
            color: var(--muted);
            line-height: 1.6;
            margin-bottom: 1rem;
        }

        .event-date {
            display: inline-block;
            padding: 0.5rem 1rem;
            background: linear-gradient(135deg, var(--primary-light), var(--primary));
            color: white;
            border-radius: 20px;
            font-size: 0.9rem;
            font-weight: 600;
        }

        /* Newsletter Section */
        .newsletter {
            max-width: 800px;
            margin: 0 auto;
            background: linear-gradient(135deg, var(--primary), var(--primary-dark));
            border-radius: 2rem;
            padding: 4rem 3rem;
            text-align: center;
            color: white;
            box-shadow: 0 20px 60px rgba(0, 123, 255, 0.4);
        }

        .newsletter h2 {
            font-family: 'Space Grotesk', sans-serif;
            font-size: 2.5rem;
            margin-bottom: 1rem;
        }

        .newsletter p {
            font-size: 1.1rem;
            margin-bottom: 2rem;
            opacity: 0.95;
        }

        .newsletter-form {
            display: flex;
            gap: 1rem;
            max-width: 600px;
            margin: 0 auto;
            flex-wrap: wrap;
            justify-content: center;
        }

        .newsletter-form input {
            flex: 1;
            min-width: 250px;
            padding: 1rem 1.5rem;
            border: none;
            border-radius: 50px;
            font-size: 1rem;
            outline: none;
        }

        .newsletter-form button {
            padding: 1rem 2.5rem;
            background: var(--foreground);
            color: var(--background);
            border: none;
            border-radius: 50px;
            font-weight: 600;
            cursor: pointer;
            transition: transform 0.3s;
        }

        .newsletter-form button:hover {
            transform: scale(1.05);
        }

        /* Footer */
        footer {
            background: var(--foreground);
            color: var(--background);
            padding: 3rem 1.5rem;
            text-align: center;
        }

        .social-links {
            display: flex;
            gap: 1.5rem;
            justify-content: center;
            margin-bottom: 1.5rem;
        }

        .social-links a {
            width: 48px;
            height: 48px;
            background: var(--primary);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: transform 0.3s, background 0.3s;
            text-decoration: none;
            color: white;
        }

        .social-links a:hover {
            transform: translateY(-5px) scale(1.1) rotate(12deg);
            background: var(--primary-dark);
        }

        /* Mobile Menu */
        .mobile-menu {
            display: none;
            flex-direction: column;
            gap: 0.5rem;
            padding: 1rem;
            background: rgba(255, 255, 255, 0.98);
            backdrop-filter: blur(10px);
            border-top: 1px solid var(--border);
        }

        [data-theme="dark"] .mobile-menu {
            background: rgba(15, 20, 25, 0.98);
        }

        .mobile-menu.active {
            display: flex;
        }

        .mobile-menu a {
            padding: 1rem;
            text-decoration: none;
            color: var(--foreground);
            font-weight: 500;
            border-radius: 0.5rem;
            transition: background 0.3s;
        }

        .mobile-menu a:hover {
            background: var(--card);
        }

        /* Responsive */
        @media (max-width: 768px) {
            .nav-links {
                display: none;
            }

            .burger {
                display: flex;
            }

            .hero h1 {
                font-size: 2.5rem;
            }

            .hero p {
                font-size: 1.1rem;
            }

            .hero-logo {
                width: 180px;
                height: 180px;
            }

            .about-content {
                grid-template-columns: 1fr;
            }

            .section-title {
                font-size: 2rem;
            }

            .newsletter h2 {
                font-size: 1.8rem;
            }
        }
    </style>
</head>
<body>
    <!-- Navigation -->
    <nav>
        <div class="nav-container">
            <div class="logo-section">
                <!-- Replace this src with your actual logo path -->
                <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Ccircle cx='50' cy='50' r='40' fill='%23007bff'/%3E%3C/svg%3E" alt="EDS Logo" class="logo-img">
                <div class="logo-text">EDS</div>
            </div>
            <div class="nav-right">
                <ul class="nav-links">
                    <li><a href="#home">Home</a></li>
                    <li><a href="#about">About</a></li>
                    <li><a href="#team">Team</a></li>
                    <li><a href="#events">Events</a></li>
                    <li><a href="#contact">Contact</a></li>
                </ul>
                <button class="theme-toggle" onclick="toggleTheme()">
                    <div class="theme-toggle-slider">☀️</div>
                </button>
                <div class="burger" onclick="toggleMobileMenu()">
                    <span></span>
                    <span></span>
                    <span></span>
                </div>
            </div>
        </div>
        <div class="mobile-menu" id="mobileMenu">
            <a href="#home" onclick="toggleMobileMenu()">Home</a>
            <a href="#about" onclick="toggleMobileMenu()">About</a>
            <a href="#team" onclick="toggleMobileMenu()">Team</a>
            <a href="#events" onclick="toggleMobileMenu()">Events</a>
            <a href="#contact" onclick="toggleMobileMenu()">Contact</a>
        </div>
    </nav>

    <!-- Hero Section -->
    <section id="home" class="hero">
        <div class="pattern-bg"></div>
        <div class="hero-gradient"></div>
        <div class="hero-content">
            <!-- Replace this src with your actual logo path -->
            <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Ccircle cx='50' cy='50' r='40' fill='%23007bff'/%3E%3C/svg%3E" alt="EDS Logo" class="hero-logo">
            <h1>Echelon Dev Society</h1>
            <p>Empowering developers, building the future. Join our community of passionate coders and innovators shaping tomorrow's technology.</p>
            <a href="#about" class="cta-button">Discover More</a>
        </div>
        <div class="scroll-indicator" onclick="document.querySelector('#about').scrollIntoView({behavior: 'smooth'})">
            <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <polyline points="6 9 12 15 18 9"></polyline>
            </svg>
        </div>
    </section>

    <!-- About Section -->
    <section id="about">
        <h2 class="section-title"><span>About EDS</span></h2>
        <div class="about-content">
            <div class="about-text">
                <h3>Who We Are</h3>
                <p>Echelon Dev Society (EDS) is a vibrant community of tech enthusiasts, developers, and innovators dedicated to fostering creativity and technical excellence. We organize workshops, hackathons, and collaborative projects that empower members to learn, build, and grow together.</p>
                <p>Our mission is to create an inclusive environment where everyone—from beginners to experts—can explore cutting-edge technologies, share knowledge, and transform ideas into reality. Join us on this exciting journey of innovation and collaboration!</p>
            </div>
            <div class="about-image"></div>
        </div>
    </section>

    <!-- Team Section -->
    <section id="team">
        <h2 class="section-title"><span>Meet Our Core Team</span></h2>
        <div class="team-grid">
            <div class="team-card">
                <div class="team-photo">
                    <!-- Replace with actual logo -->
                    <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Ccircle cx='50' cy='50' r='40' fill='%23007bff'/%3E%3C/svg%3E" alt="Alex Rivera">
                </div>
                <h3>Alex Rivera</h3>
                <p>President</p>
            </div>
            <div class="team-card">
                <div class="team-photo">
                    <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Ccircle cx='50' cy='50' r='40' fill='%23007bff'/%3E%3C/svg%3E" alt="Sarah Chen">
                </div>
                <h3>Sarah Chen</h3>
                <p>Vice President</p>
            </div>
            <div class="team-card">
                <div class="team-photo">
                    <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Ccircle cx='50' cy='50' r='40' fill='%23007bff'/%3E%3C/svg%3E" alt="Marcus Johnson">
                </div>
                <h3>Marcus Johnson</h3>
                <p>Technical Lead</p>
            </div>
            <div class="team-card">
                <div class="team-photo">
                    <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Ccircle cx='50' cy='50' r='40' fill='%23007bff'/%3E%3C/svg%3E" alt="Priya Sharma">
                </div>
                <h3>Priya Sharma</h3>
                <p>Event Coordinator</p>
            </div>
            <div class="team-card">
                <div class="team-photo">
                    <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Ccircle cx='50' cy='50' r='40' fill='%23007bff'/%3E%3C/svg%3E" alt="David Kim">
                </div>
                <h3>David Kim</h3>
                <p>Creative Director</p>
            </div>
            <div class="team-card">
                <div class="team-photo">
                    <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Ccircle cx='50' cy='50' r='40' fill='%23007bff'/%3E%3C/svg%3E" alt="Mihir Jain">
                </div>
                <h3>Mihir Jain</h3>
                <p>Media & Publicity Head</p>
            </div>
            <div class="team-card">
                <div class="team-photo">
                    <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Ccircle cx='50' cy='50' r='40' fill='%23007bff'/%3E%3C/svg%3E" alt="Emma Thompson">
                </div>
                <h3>Emma Thompson</h3>
                <p>Community Manager</p>
            </div>
            <div class="team-card">
                <div class="team-photo">
                    <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Ccircle cx='50' cy='50' r='40' fill='%23007bff'/%3E%3C/svg%3E" alt="Ryan Patel">
                </div>
                <h3>Ryan Patel</h3>
                <p>Outreach Lead</p>
            </div>
        </div>
    </section>

    <!-- Events Section -->
    <section id="events">
        <h2 class="section-title"><span>Upcoming Events</span></h2>
        <div class="events-grid">
            <div class="event-card">
                <div class="event-image" style="background: linear-gradient(135deg, rgba(0, 123, 255, 0.3), rgba(0, 86, 179, 0.3)), url('https://images.unsplash.com/photo-1540575467063-178a50c2df87?w=800&q=80') center/cover;"></div>
                <div class="event-content">
                    <h3>Hackathon 2025</h3>
                    <p>Join us for an exciting 48-hour coding marathon where teams compete to build innovative solutions.</p>
                    <span class="event-date">March 15-17, 2025</span>
                </div>
            </div>
            <div class="event-card">
                <div class="event-image" style="background: linear-gradient(135deg, rgba(0, 123, 255, 0.3), rgba(0, 86, 179, 0.3)), url('https://images.unsplash.com/photo-1517694712202-14dd9538aa97?w=800&q=80') center/cover;"></div>
                <div class="event-content">
                    <h3>Web Development Workshop</h3>
                    <p>Learn modern web development with React, TypeScript, and cutting-edge tools from industry experts.</p>
                    <span class="event-date">April 5, 2025</span>
                </div>
            </div>
            <div class="event-card">
                <div class="event-image" style="background: linear-gradient(135deg, rgba(0, 123, 255, 0.3), rgba(0, 86, 179, 0.3)), url('https://images.unsplash.com/photo-1677442136019-21780ecad995?w=800&q=80') center/cover;"></div>
                <div class="event-content">
                    <h3>AI & Machine Learning Seminar</h3>
                    <p>Explore the latest trends in artificial intelligence and machine learning with hands-on sessions.</p>
                    <span class="event-date">May 20, 2025</span>
                </div>
            </div>
            <div class="event-card">
                <div class="event-image" style="background: linear-gradient(135deg, rgba(0, 123, 255, 0.3), rgba(0, 86, 179, 0.3)), url('https://images.unsplash.com/photo-1618401471353-b98afee0b2eb?w=800&q=80') center/cover;"></div>
                <div class="event-content">
                    <h3>Open Source Contribution Drive</h3>
                    <p>Contribute to open source projects and learn collaborative development practices.</p>
                    <span class="event-date">June 10, 2025</span>
                </div>
            </div>
        </div>
    </section>

    <!-- Newsletter Section -->
    <section id="contact">
        <div class="newsletter">
            <h2>Stay Updated</h2>
            <p>Subscribe to our newsletter for the latest events, workshops, and community updates.</p>
            <form class="newsletter-form" onsubmit="handleNewsletter(event)">
                <input type="email" placeholder="Enter your email" required>
                <button type="submit">Subscribe</button>
            </form>
        </div>
    </section>

    <!-- Footer -->
    <footer>
        <div class="social-links">
            <a href="#" aria-label="GitHub">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
                </svg>
            </a>
            <a href="#" aria-label="LinkedIn">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z"/>
                </svg>
            </a>
            <a href="#" aria-label="Twitter">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M24 4.557c-.883.392-1.832.656-2.828.775 1.017-.609 1.798-1.574 2.165-2.724-.951.564-2.005.974-3.127 1.195-.897-.957-2.178-1.555-3.594-1.555-3.179 0-5.515 2.966-4.797 6.045-4.091-.205-7.719-2.165-10.148-5.144-1.29 2.213-.669 5.108 1.523 6.574-.806-.026-1.566-.247-2.229-.616-.054 2.281 1.581 4.415 3.949 4.89-.693.188-1.452.232-2.224.084.626 1.956 2.444 3.379 4.6 3.419-2.07 1.623-4.678 2.348-7.29 2.04 2.179 1.397 4.768 2.212 7.548 2.212 9.142 0 14.307-7.721 13.995-14.646.962-.695 1.797-1.562 2.457-2.549z"/>
                </svg>
            </a>
            <a href="#" aria-label="Instagram">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/>
                </svg>
            </a>
        </div>
        <p>© 2025 Echelon Dev Society. All rights reserved.</p>
    </footer>

    <script>
        // Theme Toggle
        function toggleTheme() {
            const html = document.documentElement;
            const currentTheme = html.getAttribute('data-theme');
            const newTheme = currentTheme === 'dark' ? 'light' : 'dark';
            html.setAttribute('data-theme', newTheme);
            localStorage.setItem('theme', newTheme);
            
            const slider = document.querySelector('.theme-toggle-slider');
            slider.textContent = newTheme === 'dark' ? '🌙' : '☀️';
        }

        // Mobile Menu Toggle
        function toggleMobileMenu() {
            const menu = document.getElementById('mobileMenu');
            menu.classList.toggle('active');
        }

        // Newsletter Form
        function handleNewsletter(event) {
            event.preventDefault();
            const email = event.target.querySelector('input[type="email"]').value;
            alert('Thank you for subscribing! Email: ' + email);
            event.target.reset();
        }

        // Initialize theme from localStorage
        const savedTheme = localStorage.getItem('theme') || 'light';
        document.documentElement.setAttribute('data-theme', savedTheme);
        const slider = document.querySelector('.theme-toggle-slider');
        slider.textContent = savedTheme === 'dark' ? '🌙' : '☀️';
    </script>
</body>
</html>
