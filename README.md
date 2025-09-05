<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no" />
    <title>Smart Park NCR - Complete Single Page App</title>
    <style>
        :root {
            --primary: #6366f1;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #ef4444;
            --info: #3b82f6;
            --dark-bg: #0f172a;
            --card-bg: #1e293b;
            --surface: #334155;
            --text-primary: #f8fafc;
            --text-secondary: #cbd5e1;
            --text-muted: #64748b;
            --border: #475569;
            --radius: 12px;
            --spacing: 16px;
            --transition: all 0.3s ease;
            --gradient: linear-gradient(135deg, var(--primary), #8b5cf6);
            --shadow: 0 4px 12px rgba(0,0,0,0.3);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }

        body {
            background: var(--dark-bg);
            color: var(--text-primary);
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
            line-height: 1.6;
            min-height: 100vh;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
        }

        .container {
            max-width: 390px;
            min-height: 100vh;
            margin: 0 auto;
            padding: var(--spacing);
            display: flex;
            flex-direction: column;
            gap: 20px;
            background: var(--dark-bg);
        }

        header {
            background: var(--gradient);
            border-radius: var(--radius);
            padding: 24px;
            text-align: center;
            box-shadow: var(--shadow);
            position: relative;
            overflow: hidden;
            color: white;
        }

        header::before {
            content: '';
            position: absolute;
            top: -50%;
            right: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.1), transparent);
            animation: shimmer 4s ease-in-out infinite;
        }

        @keyframes shimmer {
            0%, 100% { transform: rotate(0deg); }
            50% { transform: rotate(180deg); }
        }

        header h1 {
            font-size: 24px;
            font-weight: 800;
            margin-bottom: 4px;
            position: relative;
            z-index: 2;
        }

        header p {
            opacity: 0.9;
            font-size: 14px;
            position: relative;
            z-index: 2;
        }

        nav {
            display: flex;
            flex-wrap: wrap;
            background: var(--card-bg);
            border-radius: var(--radius);
            padding: 8px;
            box-shadow: var(--shadow);
            border: 1px solid var(--border);
            gap: 4px;
            justify-content: center;
        }

        .tab-btn {
            background: transparent;
            border: none;
            color: var(--text-muted);
            font-size: 10px;
            font-weight: 600;
            cursor: pointer;
            padding: 8px;
            border-radius: 8px;
            transition: var(--transition);
            flex: 1 1 80px;
            max-width: 90px;
            text-align: center;
            user-select: none;
        }

        .tab-btn.active {
            color: white;
            background: var(--primary);
            box-shadow: 0 2px 8px rgba(99, 102, 241, 0.4);
            font-weight: 700;
        }

        .tab-btn:hover:not(.active) {
            color: var(--text-primary);
            background: var(--surface);
        }

        main {
            flex: 1;
            background: var(--card-bg);
            border-radius: var(--radius);
            padding: var(--spacing);
            box-shadow: var(--shadow);
            border: 1px solid var(--border);
            min-height: 400px;
            overflow-y: auto;
        }

        section {
            display: none;
            animation: fadeIn 0.3s ease forwards;
        }

        section.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .card {
            background: var(--surface);
            padding: var(--spacing);
            border-radius: var(--radius);
            border: 1px solid var(--border);
            margin-bottom: 16px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.3);
        }

        .card h2 {
            font-size: 18px;
            font-weight: 700;
            color: var(--primary);
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .card p {
            color: var(--text-secondary);
            font-size: 14px;
            margin-bottom: 8px;
        }

        ul {
            list-style: none;
            padding: 0;
        }

        li {
            padding: 8px 0;
            border-bottom: 1px solid var(--border);
            color: var(--text-secondary);
            font-size: 14px;
        }

        li:last-child {
            border-bottom: none;
        }

        input, select, textarea {
            width: 100%;
            padding: 12px;
            border-radius: var(--radius);
            border: 2px solid var(--border);
            background: var(--dark-bg);
            color: var(--text-primary);
            font-size: 14px;
            outline: none;
            transition: var(--transition);
            font-family: inherit;
            margin-bottom: 12px;
        }

        input:focus, select:focus, textarea:focus {
            border-color: var(--primary);
            box-shadow: 0 0 0 4px rgba(99, 102, 241, 0.1);
        }

        label {
            display: block;
            color: var(--text-secondary);
            font-size: 14px;
            font-weight: 600;
            margin-bottom: 8px;
        }

        .btn {
            padding: 12px 20px;
            border-radius: var(--radius);
            border: none;
            background: var(--primary);
            color: white;
            font-weight: 600;
            font-size: 14px;
            cursor: pointer;
            transition: var(--transition);
            margin-right: 8px;
            margin-bottom: 8px;
        }

        .btn:hover {
            background: var(--success);
            transform: translateY(-1px);
            box-shadow: 0 4px 12px rgba(16, 185, 129, 0.4);
        }

        .btn-danger {
            background: var(--danger);
        }

        .btn-warning {
            background: var(--warning);
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 12px;
            margin: 16px 0;
        }

        .stat-item {
            background: var(--dark-bg);
            padding: 12px;
            border-radius: var(--radius);
            text-align: center;
            border: 1px solid var(--border);
        }

        .stat-value {
            font-size: 18px;
            font-weight: 800;
            color: var(--primary);
        }

        .stat-label {
            font-size: 11px;
            color: var(--text-muted);
            text-transform: uppercase;
        }

        .setting-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px 0;
            border-bottom: 1px solid var(--border);
        }

        .setting-item:last-child {
            border-bottom: none;
        }

        .toggle-switch {
            width: 40px;
            height: 20px;
            background: var(--success);
            border-radius: 10px;
            position: relative;
            cursor: pointer;
            transition: background 0.3s ease;
        }

        .toggle-switch::after {
            content: '';
            width: 16px;
            height: 16px;
            background: white;
            border-radius: 50%;
            position: absolute;
            top: 2px;
            right: 2px;
            transition: all 0.3s ease;
        }

        .toggle-switch.off {
            background: var(--border);
        }

        .toggle-switch.off::after {
            right: auto;
            left: 2px;
        }

        .profile-pic {
            width: 80px;
            height: 80px;
            background: var(--primary);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 32px;
            margin: 0 auto 16px;
        }

        .notification-item {
            background: var(--dark-bg);
            padding: 12px;
            border-radius: var(--radius);
            margin-bottom: 8px;
            border-left: 4px solid var(--primary);
        }

        .offer-card {
            background: linear-gradient(135deg, var(--warning), #d97706);
            color: white;
            padding: 16px;
            border-radius: var(--radius);
            margin-bottom: 12px;
            position: relative;
            overflow: hidden;
        }

        .offer-card::before {
            content: '';
            position: absolute;
            top: -50%;
            right: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.1), transparent);
            animation: shimmer 3s ease-in-out infinite;
        }

        .map-placeholder {
            height: 200px;
            background: var(--dark-bg);
            border: 2px dashed var(--border);
            border-radius: var(--radius);
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--text-muted);
            text-align: center;
            margin: 16px 0;
        }

        .scrollable {
            max-height: 300px;
            overflow-y: auto;
        }

        .booking-status {
            background: rgba(16, 185, 129, 0.1);
            border: 1px solid var(--success);
            border-radius: var(--radius);
            padding: 16px;
            margin: 16px 0;
        }

        .booking-status.expired {
            background: rgba(239, 68, 68, 0.1);
            border-color: var(--danger);
        }

        @media (max-width: 430px) {
            .container {
                max-width: 100vw;
                padding: 12px;
            }

            header h1 {
                font-size: 20px;
            }

            .tab-btn {
                font-size: 9px;
                padding: 6px;
                max-width: 70px;
            }

            .stats-grid {
                grid-template-columns: repeat(2, 1fr);
            }
        }
    </style>
</head>
<body>
<div class="container">
    <header>
        <h1>🚗 Smart Park NCR</h1>
        <p>Welcome, Vatsal Gupta! Your ultimate parking solution</p>
    </header>

    <nav>
        <button class="tab-btn active" data-tab="Home_Dashboard">🏠 Home</button>
        <button class="tab-btn" data-tab="Search_Results">🔍 Search</button>
        <button class="tab-btn" data-tab="Interactive_Map_View">🗺️ Map</button>
        <button class="tab-btn" data-tab="Advanced_Wallet">💰 Wallet</button>
        <button class="tab-btn" data-tab="Booking_Confirmation">📋 Booking</button>
        <button class="tab-btn" data-tab="Booking_History">📜 History</button>
        <button class="tab-btn" data-tab="Vehicle_Management">🚗 Vehicles</button>
        <button class="tab-btn" data-tab="Notifications_Center">🔔 Alerts</button>
        <button class="tab-btn" data-tab="Offers_and_Promotions">🎉 Offers</button>
        <button class="tab-btn" data-tab="Payment_Gateway">💳 Payment</button>
        <button class="tab-btn" data-tab="Settings">⚙️ Settings</button>
        <button class="tab-btn" data-tab="User_Profile">👤 Profile</button>
        <button class="tab-btn" data-tab="Comprehensive_Support_Center">🛠️ Support</button>
    </nav>

    <main>
        <!-- Home Dashboard -->
        <section id="Home_Dashboard" class="active">
            <div class="card">
                <h2>🏠 Dashboard Overview</h2>
                <p>Welcome back, <strong>Vatsal Gupta</strong>! Here's your parking summary:</p>

                <div class="stats-grid">
                    <div class="stat-item">
                        <div class="stat-value">₹1,250</div>
                        <div class="stat-label">Wallet Balance</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value">47</div>
                        <div class="stat-label">Total Bookings</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value">4.9★</div>
                        <div class="stat-label">User Rating</div>
                    </div>
                </div>

                <div class="booking-status">
                    <h3 style="color: var(--success); margin-bottom: 8px;">🚗 Active Booking</h3>
                    <p><strong>Location:</strong> Connaught Place Metro Station</p>
                    <p><strong>Vehicle:</strong> Honda City (DL01AB1234)</p>
                    <p><strong>Time Remaining:</strong> 1h 32m</p>
                    <button class="btn">Extend Booking</button>
                    <button class="btn btn-warning">Navigate</button>
                </div>
            </div>

            <div class="card">
                <h2>⚡ Quick Actions</h2>
                <button class="btn" onclick="switchTab('Search_Results')">🔍 Find Parking</button>
                <button class="btn" onclick="switchTab('Advanced_Wallet')">💰 Add Money</button>
                <button class="btn" onclick="switchTab('Interactive_Map_View')">🗺️ View Map</button>
                <button class="btn" onclick="switchTab('Booking_History')">📜 View History</button>
            </div>
        </section>

        <!-- Search Results -->
        <section id="Search_Results">
            <div class="card">
                <h2>🔍 Find Parking Spots</h2>
                <form onsubmit="searchParking(event)">
                    <label for="search-location">📍 Location</label>
                    <input type="text" id="search-location" placeholder="Enter destination, landmark, or area" value="Connaught Place" />

                    <label for="search-vehicle">🚗 Select Vehicle</label>
                    <select id="search-vehicle">
                        <option value="car1">Honda City - DL01AB1234</option>
                        <option value="bike1">Royal Enfield - DL05CD5678</option>
                        <option value="car2">Maruti Swift - DL10XY9876</option>
                    </select>

                    <label for="search-duration">⏰ Parking Duration</label>
                    <select id="search-duration">
                        <option value="1">1 Hour - ₹30</option>
                        <option value="2">2 Hours - ₹55</option>
                        <option value="4">4 Hours - ₹100</option>
                        <option value="8">Full Day - ₹180</option>
                        <option value="custom">Custom Duration</option>
                    </select>

                    <button type="submit" class="btn">🔍 Search Available Spots</button>
                </form>
            </div>

            <div class="card">
                <h2>📍 Available Parking Spots</h2>
                <div class="scrollable">
                    <div style="background: var(--dark-bg); padding: 12px; border-radius: 8px; margin-bottom: 8px; border-left: 4px solid var(--success);">
                        <p><strong>Connaught Place Metro</strong> - ₹30/hr</p>
                        <p>🟢 Available • 2.3km away • 4.8★ rating</p>
                        <button class="btn" style="margin-top: 8px;">Book Now</button>
                    </div>
                    <div style="background: var(--dark-bg); padding: 12px; border-radius: 8px; margin-bottom: 8px; border-left: 4px solid var(--warning);">
                        <p><strong>Rajiv Chowk Underground</strong> - ₹25/hr</p>
                        <p>🟡 3 spots left • 1.8km away • 4.6★ rating</p>
                        <button class="btn" style="margin-top: 8px;">Book Now</button>
                    </div>
                    <div style="background: var(--dark-bg); padding: 12px; border-radius: 8px; margin-bottom: 8px; border-left: 4px solid var(--primary);">
                        <p><strong>Select City Walk Mall</strong> - ₹40/hr</p>
                        <p>🔵 Premium • 3.5km away • 4.9★ rating</p>
                        <button class="btn" style="margin-top: 8px;">Book Now</button>
                    </div>
                    <div style="background: var(--dark-bg); padding: 12px; border-radius: 8px; margin-bottom: 8px; border-left: 4px solid var(--success);">
                        <p><strong>India Gate Parking</strong> - ₹20/hr</p>
                        <p>🟢 Available • 4.2km away • 4.4★ rating</p>
                        <button class="btn" style="margin-top: 8px;">Book Now</button>
                    </div>
                    <div style="background: var(--dark-bg); padding: 12px; border-radius: 8px; margin-bottom: 8px; border-left: 4px solid var(--info);">
                        <p><strong>IGI Airport Terminal 3</strong> - ₹100/hr</p>
                        <p>🔵 Premium • 12.8km away • 4.7★ rating</p>
                        <button class="btn" style="margin-top: 8px;">Book Now</button>
                    </div>
                </div>
            </div>
        </section>

        <!-- Interactive Map View -->
        <section id="Interactive_Map_View">
            <div class="card">
                <h2>🗺️ Interactive Parking Map</h2>
                <p>Real-time parking availability in your area</p>

                <div class="map-placeholder">
                    <div>
                        🗺️<br>
                        <strong>Live Parking Map</strong><br>
                        <span style="color: var(--success);">● 45 spots available</span><br>
                        <span style="color: var(--warning);">● 12 spots filling up</span><br>
                        <span style="color: var(--danger);">● 8 spots full</span><br>
                        <small>Interactive map loads here</small>
                    </div>
                </div>

                <div style="background: var(--dark-bg); padding: 12px; border-radius: 8px; margin: 12px 0;">
                    <p><strong>📍 Your Current Location:</strong> Lajpat Nagar, New Delhi</p>
                    <p><strong>🎯 Nearby Parking:</strong> 45 available spots within 5km</p>
                    <p><strong>💰 Price Range:</strong> ₹20-150 per hour</p>
                    <p><strong>⭐ Average Rating:</strong> 4.6 stars</p>
                </div>

                <button class="btn">📍 Enable GPS Location</button>
                <button class="btn">🔍 Search Area</button>
                <button class="btn">🧭 Navigate to Selected Spot</button>
            </div>
        </section>

        <!-- Advanced Wallet -->
        <section id="Advanced_Wallet">
            <div class="card">
                <h2>💰 Smart Wallet</h2>
                <div style="text-align: center; margin: 20px 0; padding: 20px; background: var(--dark-bg); border-radius: 12px;">
                    <div style="font-size: 36px; font-weight: 800; color: var(--primary);">₹1,250.75</div>
                    <div style="color: var(--text-muted); margin-top: 4px;">Available Balance</div>
                    <div style="color: var(--success); font-size: 12px; margin-top: 8px;">✓ Auto-recharge enabled at ₹100</div>
                </div>

                <div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 12px; margin: 16px 0;">
                    <button class="btn">➕ Add Money</button>
                    <button class="btn">📊 Transactions</button>
                    <button class="btn">🎁 Rewards</button>
                    <button class="btn">⚙️ Auto-recharge</button>
                </div>
            </div>

            <div class="card">
                <h2>💳 Recent Transactions</h2>
                <div class="scrollable">
                    <div style="display: flex; justify-content: space-between; padding: 8px 0; border-bottom: 1px solid var(--border);">
                        <span>🚗 Metro Station Parking</span>
                        <span style="color: var(--danger);">-₹60</span>
                    </div>
                    <div style="display: flex; justify-content: space-between; padding: 8px 0; border-bottom: 1px solid var(--border);">
                        <span>➕ UPI Recharge</span>
                        <span style="color: var(--success);">+₹500</span>
                    </div>
                    <div style="display: flex; justify-content: space-between; padding: 8px 0; border-bottom: 1px solid var(--border);">
                        <span>🎁 Referral Reward</span>
                        <span style="color: var(--success);">+₹50</span>
                    </div>
                    <div style="display: flex; justify-content: space-between; padding: 8px 0; border-bottom: 1px solid var(--border);">
                        <span>🏪 Mall Parking</span>
                        <span style="color: var(--danger);">-₹120</span>
                    </div>
                    <div style="display: flex; justify-content: space-between; padding: 8px 0; border-bottom: 1px solid var(--border);">
                        <span>🔄 Auto-recharge</span>
                        <span style="color: var(--success);">+₹300</span>
                    </div>
                </div>

                <div style="margin-top: 16px; padding: 12px; background: var(--dark-bg); border-radius: 8px;">
                    <p><strong>💡 Smart Insights:</strong></p>
                    <p>• Average spending: ₹280/week</p>
                    <p>• Most used: Metro stations (60%)</p>
                    <p>• Savings this month: ₹150 with offers</p>
                </div>
            </div>
        </section>

        <!-- Booking Confirmation -->
        <section id="Booking_Confirmation">
            <div class="card">
                <h2>✅ Active Booking</h2>
                <div class="booking-status">
                    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 16px;">
                        <h3 style="color: var(--success);">🟢 CONFIRMED</h3>
                        <span style="background: var(--success); color: white; padding: 4px 8px; border-radius: 12px; font-size: 12px;">ACTIVE</span>
                    </div>

                    <div style="margin-bottom: 16px;">
                        <p><strong>📍 Location:</strong> Connaught Place Metro Station, Gate 4</p>
                        <p><strong>🚗 Vehicle:</strong> Honda City (DL01AB1234)</p>
                        <p><strong>🕐 Start Time:</strong> Today, 2:15 PM</p>
                        <p><strong>⏰ End Time:</strong> Today, 6:15 PM</p>
                        <p><strong>⏱️ Time Remaining:</strong> <span style="color: var(--warning); font-weight: 700;">1h 32m</span></p>
                        <p><strong>💰 Amount Paid:</strong> ₹120</p>
                    </div>

                    <div style="background: var(--dark-bg); padding: 12px; border-radius: 8px; margin: 12px 0;">
                        <p><strong>🎫 Booking ID:</strong> SPK240906001</p>
                        <p><strong>📱 QR Code:</strong> Show to parking attendant</p>
                        <div style="width: 80px; height: 80px; background: white; margin: 8px auto; border-radius: 8px; display: flex; align-items: center; justify-content: center; color: black; font-weight: bold;">QR</div>
                    </div>

                    <button class="btn">⏰ Extend Booking (+1 Hour)</button>
                    <button class="btn btn-warning">🧭 Navigate to Location</button>
                    <button class="btn btn-danger">❌ Cancel Booking</button>
                </div>
            </div>

            <div class="card">
                <h2>📞 Quick Support</h2>
                <p>Need help with your booking?</p>
                <button class="btn">📞 Call Support</button>
                <button class="btn">💬 Live Chat</button>
                <button class="btn">📧 Email Help</button>
            </div>
        </section>

        <!-- Booking History -->
        <section id="Booking_History">
            <div class="card">
                <h2>📜 Booking History</h2>
                <div style="display: flex; gap: 8px; margin-bottom: 16px;">
                    <button class="btn" onclick="filterHistory('all')">All</button>
                    <button class="btn" onclick="filterHistory('completed')">Completed</button>
                    <button class="btn" onclick="filterHistory('cancelled')">Cancelled</button>
                </div>

                <div class="scrollable">
                    <div style="background: var(--dark-bg); padding: 12px; border-radius: 8px; margin-bottom: 8px; border-left: 4px solid var(--success);">
                        <div style="display: flex; justify-content: space-between; align-items: start;">
                            <div>
                                <p><strong>Central Mall Parking</strong></p>
                                <p style="font-size: 12px; color: var(--text-muted);">Nov 2, 2024 • 2:30 PM - 6:30 PM</p>
                                <p style="font-size: 12px;">Honda City • 4 hours</p>
                            </div>
                            <div style="text-align: right;">
                                <p style="color: var(--success); font-weight: 600;">₹160</p>
                                <span style="background: var(--success); color: white; padding: 2px 6px; border-radius: 8px; font-size: 10px;">COMPLETED</span>
                            </div>
                        </div>
                        <button class="btn" style="margin-top: 8px; padding: 6px 12px; font-size: 12px;">Book Again</button>
                    </div>

                    <div style="background: var(--dark-bg); padding: 12px; border-radius: 8px; margin-bottom: 8px; border-left: 4px solid var(--success);">
                        <div style="display: flex; justify-content: space-between; align-items: start;">
                            <div>
                                <p><strong>Office Complex B-Block</strong></p>
                                <p style="font-size: 12px; color: var(--text-muted);">Nov 3, 2024 • 9:00 AM - 6:00 PM</p>
                                <p style="font-size: 12px;">Honda City • 9 hours</p>
                            </div>
                            <div style="text-align: right;">
                                <p style="color: var(--success); font-weight: 600;">₹200</p>
                                <span style="background: var(--success); color: white; padding: 2px 6px; border-radius: 8px; font-size: 10px;">COMPLETED</span>
                            </div>
                        </div>
                        <button class="btn" style="margin-top: 8px; padding: 6px 12px; font-size: 12px;">Book Again</button>
                    </div>

                    <div style="background: var(--dark-bg); padding: 12px; border-radius: 8px; margin-bottom: 8px; border-left: 4px solid var(--danger);">
                        <div style="display: flex; justify-content: space-between; align-items: start;">
                            <div>
                                <p><strong>Rajiv Chowk Metro</strong></p>
                                <p style="font-size: 12px; color: var(--text-muted);">Oct 20, 2024 • 3:00 PM - 7:00 PM</p>
                                <p style="font-size: 12px;">Royal Enfield • 4 hours</p>
                            </div>
                            <div style="text-align: right;">
                                <p style="color: var(--danger); font-weight: 600;">₹60</p>
                                <span style="background: var(--danger); color: white; padding: 2px 6px; border-radius: 8px; font-size: 10px;">CANCELLED</span>
                            </div>
                        </div>
                        <p style="font-size: 12px; color: var(--text-muted); margin-top: 4px;">Refunded: ₹45 • Cancellation fee: ₹15</p>
                    </div>

                    <div style="background: var(--dark-bg); padding: 12px; border-radius: 8px; margin-bottom: 8px; border-left: 4px solid var(--success);">
                        <div style="display: flex; justify-content: space-between; align-items: start;">
                            <div>
                                <p><strong>India Gate Parking</strong></p>
                                <p style="font-size: 12px; color: var(--text-muted);">Oct 15, 2024 • 11:00 AM - 3:00 PM</p>
                                <p style="font-size: 12px;">Honda City • 4 hours</p>
                            </div>
                            <div style="text-align: right;">
                                <p style="color: var(--success); font-weight: 600;">₹80</p>
                                <span style="background: var(--success); color: white; padding: 2px 6px; border-radius: 8px; font-size: 10px;">COMPLETED</span>
                            </div>
                        </div>
                        <button class="btn" style="margin-top: 8px; padding: 6px 12px; font-size: 12px;">Book Again</button>
                    </div>
                </div>

                <div style="margin-top: 16px; padding: 12px; background: var(--dark-bg); border-radius: 8px;">
                    <p><strong>📊 Parking Statistics:</strong></p>
                    <p>• Total bookings: 47</p>
                    <p>• Successful bookings: 44 (93.6%)</p>
                    <p>• Total amount spent: ₹3,480</p>
                    <p>• Average rating given: 4.7★</p>
                </div>
            </div>
        </section>

        <!-- Vehicle Management -->
        <section id="Vehicle_Management">
            <div class="card">
                <h2>🚗 My Vehicles</h2>
                <p>Manage your registered vehicles for quick booking</p>

                <div style="background: var(--dark-bg); padding: 16px; border-radius: 8px; margin: 12px 0; border-left: 4px solid var(--primary);">
                    <div style="display: flex; justify-content: space-between; align-items: start;">
                        <div>
                            <h3 style="color: var(--primary);">🚗 Honda City</h3>
                            <p><strong>Registration:</strong> DL01AB1234</p>
                            <p><strong>Type:</strong> Sedan • Color: White</p>
                            <p><strong>Insurance:</strong> Valid till Dec 2025</p>
                            <p><strong>Status:</strong> <span style="color: var(--success);">✅ Verified</span></p>
                        </div>
                        <div>
                            <span style="background: var(--primary); color: white; padding: 4px 8px; border-radius: 8px; font-size: 10px;">PRIMARY</span>
                        </div>
                    </div>
                    <button class="btn" style="margin-top: 8px;">✏️ Edit Details</button>
                </div>

                <div style="background: var(--dark-bg); padding: 16px; border-radius: 8px; margin: 12px 0; border-left: 4px solid var(--success);">
                    <div style="display: flex; justify-content: space-between; align-items: start;">
                        <div>
                            <h3 style="color: var(--success);">🏍️ Royal Enfield Classic</h3>
                            <p><strong>Registration:</strong> DL05CD5678</p>
                            <p><strong>Type:</strong> Motorcycle • Color: Black</p>
                            <p><strong>Insurance:</strong> Valid till Aug 2025</p>
                            <p><strong>Status:</strong> <span style="color: var(--success);">✅ Verified</span></p>
                        </div>
                    </div>
                    <button class="btn" style="margin-top: 8px;">✏️ Edit Details</button>
                </div>

                <div style="background: var(--dark-bg); padding: 16px; border-radius: 8px; margin: 12px 0; border-left: 4px solid var(--warning);">
                    <div style="display: flex; justify-content: space-between; align-items: start;">
                        <div>
                            <h3 style="color: var(--warning);">🚗 Maruti Swift</h3>
                            <p><strong>Registration:</strong> DL10XY9876</p>
                            <p><strong>Type:</strong> Hatchback • Color: Red</p>
                            <p><strong>Insurance:</strong> Expires in 2 months</p>
                            <p><strong>Status:</strong> <span style="color: var(--warning);">⚠️ Documents Pending</span></p>
                        </div>
                    </div>
                    <button class="btn btn-warning" style="margin-top: 8px;">📄 Upload Documents</button>
                </div>

                <button class="btn">➕ Add New Vehicle</button>
            </div>

            <div class="card">
                <h2>📋 Vehicle Requirements</h2>
                <ul>
                    <li>✅ Valid Registration Certificate (RC)</li>
                    <li>✅ Valid Insurance Policy</li>
                    <li>✅ Pollution Under Control (PUC) Certificate</li>
                    <li>✅ Clear photos of vehicle and number plate</li>
                    <li>ℹ️ Verification takes 24-48 hours</li>
                </ul>
            </div>
        </section>

        <!-- Notifications Center -->
        <section id="Notifications_Center">
            <div class="card">
                <h2>🔔 Notifications</h2>
                <div style="display: flex; gap: 8px; margin-bottom: 16px;">
                    <button class="btn" onclick="filterNotifications('all')">All (8)</button>
                    <button class="btn" onclick="filterNotifications('unread')">Unread (3)</button>
                    <button class="btn" onclick="filterNotifications('important')">Important</button>
                </div>

                <div class="scrollable">
                    <div class="notification-item" style="border-left-color: var(--danger);">
                        <div style="display: flex; justify-content: space-between; align-items: start; margin-bottom: 8px;">
                            <h4 style="color: var(--danger);">🚨 Booking Expires Soon</h4>
                            <span style="font-size: 12px; color: var(--text-muted);">5 min ago</span>
                        </div>
                        <p>Your parking at Connaught Place Metro expires in 30 minutes. Extend now to avoid penalties.</p>
                        <button class="btn" style="margin-top: 8px; padding: 6px 12px; font-size: 12px;">Extend Booking</button>
                    </div>

                    <div class="notification-item" style="border-left-color: var(--success);">
                        <div style="display: flex; justify-content: space-between; align-items: start; margin-bottom: 8px;">
                            <h4 style="color: var(--success);">✅ Payment Successful</h4>
                            <span style="font-size: 12px; color: var(--text-muted);">2 hours ago</span>
                        </div>
                        <p>₹120 debited from Smart Wallet for Connaught Place Metro parking. Receipt sent to email.</p>
                    </div>

                    <div class="notification-item" style="border-left-color: var(--warning);">
                        <div style="display: flex; justify-content: space-between; align-items: start; margin-bottom: 8px;">
                            <h4 style="color: var(--warning);">🔔 Wallet Balance Low</h4>
                            <span style="font-size: 12px; color: var(--text-muted);">1 day ago</span>
                        </div>
                        <p>Your wallet balance is ₹50. Recharge now to avoid booking failures. Auto-recharge available.</p>
                        <button class="btn" style="margin-top: 8px; padding: 6px 12px; font-size: 12px;">Add Money</button>
                    </div>

                    <div class="notification-item" style="border-left-color: var(--info);">
                        <div style="display: flex; justify-content: space-between; align-items: start; margin-bottom: 8px;">
                            <h4 style="color: var(--info);">🎉 Special Offer</h4>
                            <span style="font-size: 12px; color: var(--text-muted);">2 days ago</span>
                        </div>
                        <p>Weekend Special: 50% off on all mall parking! Use code WEEKEND50. Valid till Sunday.</p>
                        <button class="btn" style="margin-top: 8px; padding: 6px 12px; font-size: 12px;">Use Offer</button>
                    </div>

                    <div class="notification-item">
                        <div style="display: flex; justify-content: space-between; align-items: start; margin-bottom: 8px;">
                            <h4>📍 New Parking Location</h4>
                            <span style="font-size: 12px; color: var(--text-muted);">3 days ago</span>
                        </div>
                        <p>New parking facility added near DLF Cyber City. 200 spots available with premium amenities.</p>
                    </div>

                    <div class="notification-item">
                        <div style="display: flex; justify-content: space-between; align-items: start; margin-bottom: 8px;">
                            <h4>🚗 Vehicle Verification Complete</h4>
                            <span style="font-size: 12px; color: var(--text-muted);">5 days ago</span>
                        </div>
                        <p>Your Honda City (DL01AB1234) has been successfully verified. You can now book parking spots.</p>
                    </div>
                </div>

                <div style="margin-top: 16px;">
                    <button class="btn">✅ Mark All as Read</button>
                    <button class="btn">🗑️ Clear Notifications</button>
                    <button class="btn">⚙️ Notification Settings</button>
                </div>
            </div>
        </section>

        <!-- Offers and Promotions -->
        <section id="Offers_and_Promotions">
            <div class="card">
                <h2>🎉 Special Offers & Promotions</h2>
                <p>Save more on your parking with exclusive deals!</p>

                <div class="offer-card">
                    <div style="position: relative; z-index: 2;">
                        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 12px;">
                            <h3>🎊 Weekend Special</h3>
                            <span style="background: rgba(255,255,255,0.2); padding: 4px 8px; border-radius: 12px; font-size: 12px; font-weight: 700;">50% OFF</span>
                        </div>
                        <p style="margin-bottom: 12px; opacity: 0.9;">Get 50% discount on all mall parking this weekend. Valid at Select City Walk, DLF Malls, and more!</p>
                        <div style="display: flex; gap: 8px; align-items: center;">
                            <span style="font-size: 14px; font-weight: 600;">Code: WEEKEND50</span>
                            <button class="btn" style="background: rgba(255,255,255,0.2); color: white; border: 1px solid white;">Use Now</button>
                        </div>
                    </div>
                </div>

                <div style="background: linear-gradient(135deg, var(--success), #047857); color: white; padding: 16px; border-radius: 12px; margin: 12px 0; position: relative; overflow: hidden;">
                    <div style="position: relative; z-index: 2;">
                        <h3>💰 Wallet Bonus Offer</h3>
                        <p style="margin: 8px 0; opacity: 0.9;">Recharge ₹500 or more and get ₹50 bonus instantly!</p>
                        <div style="display: flex; gap: 8px; align-items: center;">
                            <span style="font-size: 12px; opacity: 0.8;">Valid till: Dec 31, 2024</span>
                            <button class="btn" style="background: rgba(255,255,255,0.2); color: white; border: 1px solid white;">Recharge Now</button>
                        </div>
                    </div>
                </div>

                <div style="background: linear-gradient(135deg, var(--info), #1e40af); color: white; padding: 16px; border-radius: 12px; margin: 12px 0;">
                    <h3>🤝 Refer & Earn</h3>
                    <p style="margin: 8px 0; opacity: 0.9;">Invite friends and earn ₹100 credit when they make their first booking!</p>
                    <div style="display: flex; gap: 8px; align-items: center;">
                        <span style="font-size: 12px; opacity: 0.8;">Unlimited referrals</span>
                        <button class="btn" style="background: rgba(255,255,255,0.2); color: white; border: 1px solid white;">Share Link</button>
                    </div>
                </div>

                <div class="card" style="background: var(--dark-bg);">
                    <h3>🏆 Loyalty Program - Smart Plus</h3>
                    <p>Earn points on every booking and unlock exclusive benefits!</p>
                    <div style="margin: 12px 0;">
                        <div style="display: flex; justify-content: space-between; margin-bottom: 8px;">
                            <span>Current Points:</span>
                            <span style="color: var(--primary); font-weight: 600;">2,450 points</span>
                        </div>
                        <div style="background: var(--border); height: 8px; border-radius: 4px; overflow: hidden;">
                            <div style="background: var(--primary); height: 100%; width: 80%;"></div>
                        </div>
                        <p style="font-size: 12px; color: var(--text-muted); margin-top: 4px;">550 points to reach Gold tier</p>
                    </div>
                    <button class="btn">🎁 Redeem Points</button>
                </div>

                <div class="card" style="background: var(--dark-bg);">
                    <h3>📱 Available Coupons</h3>
                    <div style="display: flex; justify-content: space-between; align-items: center; margin: 8px 0; padding: 8px 0; border-bottom: 1px solid var(--border);">
                        <div>
                            <p><strong>FIRST50</strong> - ₹50 off on first booking</p>
                            <p style="font-size: 12px; color: var(--text-muted);">Min booking: ₹100</p>
                        </div>
                        <button class="btn" style="padding: 6px 12px; font-size: 12px;">Apply</button>
                    </div>
                    <div style="display: flex; justify-content: space-between; align-items: center; margin: 8px 0; padding: 8px 0; border-bottom: 1px solid var(--border);">
                        <div>
                            <p><strong>METRO25</strong> - 25% off metro parking</p>
                            <p style="font-size: 12px; color: var(--text-muted);">Valid for 7 days</p>
                        </div>
                        <button class="btn" style="padding: 6px 12px; font-size: 12px;">Apply</button>
                    </div>
                </div>
            </div>
        </section>

        <!-- Payment Gateway -->
        <section id="Payment_Gateway">
            <div class="card">
                <h2>💳 Secure Payment Gateway</h2>
                <div style="background: var(--dark-bg); padding: 16px; border-radius: 8px; margin: 12px 0;">
                    <h3>Payment Summary</h3>
                    <div style="display: flex; justify-content: space-between; margin: 8px 0;">
                        <span>Parking Fee (4 hours):</span>
                        <span>₹120.00</span>
                    </div>
                    <div style="display: flex; justify-content: space-between; margin: 8px 0; color: var(--success);">
                        <span>Weekend Discount (50%):</span>
                        <span>-₹60.00</span>
                    </div>
                    <div style="display: flex; justify-content: space-between; margin: 8px 0;">
                        <span>Service Fee:</span>
                        <span>₹5.00</span>
                    </div>
                    <hr style="margin: 12px 0; border-color: var(--border);">
                    <div style="display: flex; justify-content: space-between; font-size: 18px; font-weight: 700; color: var(--primary);">
                        <span>Total Amount:</span>
                        <span>₹65.00</span>
                    </div>
                </div>

                <h3>Choose Payment Method:</h3>

                <div style="background: var(--dark-bg); padding: 12px; border-radius: 8px; margin: 8px 0; border: 2px solid var(--primary);">
                    <label style="display: flex; align-items: center; gap: 12px; cursor: pointer;">
                        <input type="radio" name="payment" value="wallet" checked style="width: auto;">
                        <div>
                            <h4 style="color: var(--primary);">💰 Smart Wallet</h4>
                            <p style="font-size: 12px; color: var(--text-muted);">Balance: ₹1,250.75</p>
                        </div>
                    </label>
                </div>

                <div style="background: var(--dark-bg); padding: 12px; border-radius: 8px; margin: 8px 0;">
                    <label style="display: flex; align-items: center; gap: 12px; cursor: pointer;">
                        <input type="radio" name="payment" value="upi" style="width: auto;">
                        <div>
                            <h4>📱 UPI Payment</h4>
                            <p style="font-size: 12px; color: var(--text-muted);">vatsalgupta@paytm</p>
                        </div>
                    </label>
                </div>

                <div style="background: var(--dark-bg); padding: 12px; border-radius: 8px; margin: 8px 0;">
                    <label style="display: flex; align-items: center; gap: 12px; cursor: pointer;">
                        <input type="radio" name="payment" value="card" style="width: auto;">
                        <div>
                            <h4>💳 Credit/Debit Card</h4>
                            <p style="font-size: 12px; color: var(--text-muted);">**** **** **** 1234 (HDFC)</p>
                        </div>
                    </label>
                </div>

                <div style="background: var(--dark-bg); padding: 12px; border-radius: 8px; margin: 8px 0;">
                    <label style="display: flex; align-items: center; gap: 12px; cursor: pointer;">
                        <input type="radio" name="payment" value="netbanking" style="width: auto;">
                        <div>
                            <h4>🏦 Net Banking</h4>
                            <p style="font-size: 12px; color: var(--text-muted);">Choose your bank</p>
                        </div>
                    </label>
                </div>

                <div style="margin: 16px 0;">
                    <label>
                        <input type="checkbox" checked style="width: auto; margin-right: 8px;">
                        Save this payment method for future bookings
                    </label>
                </div>

                <div style="background: rgba(16, 185, 129, 0.1); border: 1px solid var(--success); padding: 12px; border-radius: 8px; margin: 16px 0;">
                    <p style="color: var(--success); font-size: 14px;">🔒 Your payment is secured with 256-bit SSL encryption</p>
                </div>

                <button class="btn" style="width: 100%; font-size: 16px; padding: 16px;">💳 Pay ₹65.00 Securely</button>
            </div>
        </section>

        <!-- Settings -->
        <section id="Settings">
            <div class="card">
                <h2>⚙️ App Settings</h2>

                <div class="setting-item">
                    <span>🔔 Push Notifications</span>
                    <div class="toggle-switch" onclick="toggleSetting(this)"></div>
                </div>
                <div class="setting-item">
                    <span>📍 Location Services</span>
                    <div class="toggle-switch" onclick="toggleSetting(this)"></div>
                </div>
                <div class="setting-item">
                    <span>🌙 Dark Mode</span>
                    <div class="toggle-switch" onclick="toggleSetting(this)"></div>
                </div>
                <div class="setting-item">
                    <span>🔄 Auto-Recharge Wallet</span>
                    <div class="toggle-switch off" onclick="toggleSetting(this)"></div>
                </div>
                <div class="setting-item">
                    <span>📱 Haptic Feedback</span>
                    <div class="toggle-switch" onclick="toggleSetting(this)"></div>
                </div>
                <div class="setting-item">
                    <span>🔊 Sound Effects</span>
                    <div class="toggle-switch off" onclick="toggleSetting(this)"></div>
                </div>
            </div>

            <div class="card">
                <h2>🌐 Language & Region</h2>
                <label>App Language</label>
                <select>
                    <option>🇺🇸 English</option>
                    <option>🇮🇳 हिन्दी (Hindi)</option>
                    <option>🇮🇳 اردو (Urdu)</option>
                </select>

                <label>Currency</label>
                <select>
                    <option>₹ Indian Rupee (INR)</option>
                    <option>$ US Dollar (USD)</option>
                    <option>€ Euro (EUR)</option>
                </select>

                <label>Time Format</label>
                <select>
                    <option>12-hour (2:30 PM)</option>
                    <option>24-hour (14:30)</option>
                </select>
            </div>

            <div class="card">
                <h2>🔐 Privacy & Security</h2>
                <button class="btn">🔑 Change Password</button>
                <button class="btn">📱 Two-Factor Authentication</button>
                <button class="btn">🔒 Privacy Settings</button>
                <button class="btn">📊 Download My Data</button>
            </div>

            <div class="card">
                <h2>⚠️ Danger Zone</h2>
                <button class="btn btn-warning">🔄 Reset App Settings</button>
                <button class="btn btn-danger">🗑️ Delete Account</button>
            </div>
        </section>

        <!-- User Profile -->
        <section id="User_Profile">
            <div class="card">
                <h2>👤 User Profile</h2>
                <div style="text-align: center; margin: 20px 0;">
                    <div class="profile-pic">👨</div>
                    <h3 style="color: var(--primary);">Vatsal Gupta</h3>
                    <p style="color: var(--text-muted);">Smart Park NCR Member since Jan 2024</p>
                </div>

                <div style="background: var(--dark-bg); padding: 16px; border-radius: 8px; margin: 16px 0;">
                    <div style="display: flex; justify-content: space-between; margin: 8px 0;">
                        <span>📧 Email:</span>
                        <span>vatsal.gupta@example.com</span>
                    </div>
                    <div style="display: flex; justify-content: space-between; margin: 8px 0;">
                        <span>📱 Phone:</span>
                        <span>+91 98765 43210</span>
                    </div>
                    <div style="display: flex; justify-content: space-between; margin: 8px 0;">
                        <span>📍 City:</span>
                        <span>New Delhi, India</span>
                    </div>
                    <div style="display: flex; justify-content: space-between; margin: 8px 0;">
                        <span>🎂 Date of Birth:</span>
                        <span>March 15, 1995</span>
                    </div>
                </div>

                <button class="btn">✏️ Edit Profile</button>
                <button class="btn">📷 Change Profile Picture</button>
            </div>

            <div class="card">
                <h2>📊 Account Statistics</h2>
                <div class="stats-grid">
                    <div class="stat-item">
                        <div class="stat-value">47</div>
                        <div class="stat-label">Total Bookings</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value">₹3,480</div>
                        <div class="stat-label">Total Spent</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value">4.9★</div>
                        <div class="stat-label">User Rating</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value">2,450</div>
                        <div class="stat-label">Reward Points</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value">₹520</div>
                        <div class="stat-label">Total Savings</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value">Silver</div>
                        <div class="stat-label">Tier Status</div>
                    </div>
                </div>
            </div>

            <div class="card">
                <h2>🏆 Achievements</h2>
                <div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 12px;">
                    <div style="background: var(--dark-bg); padding: 12px; border-radius: 8px; text-align: center;">
                        <div style="font-size: 24px; margin-bottom: 8px;">🎯</div>
                        <p style="font-size: 12px; font-weight: 600;">First Booking</p>
                    </div>
                    <div style="background: var(--dark-bg); padding: 12px; border-radius: 8px; text-align: center;">
                        <div style="font-size: 24px; margin-bottom: 8px;">🔥</div>
                        <p style="font-size: 12px; font-weight: 600;">10 Bookings</p>
                    </div>
                    <div style="background: var(--dark-bg); padding: 12px; border-radius: 8px; text-align: center;">
                        <div style="font-size: 24px; margin-bottom: 8px;">💎</div>
                        <p style="font-size: 12px; font-weight: 600;">VIP Member</p>
                    </div>
                    <div style="background: var(--dark-bg); padding: 12px; border-radius: 8px; text-align: center;">
                        <div style="font-size: 24px; margin-bottom: 8px;">🌟</div>
                        <p style="font-size: 12px; font-weight: 600;">5★ Rating</p>
                    </div>
                </div>
            </div>
        </section>

        <!-- Comprehensive Support Center -->
        <section id="Comprehensive_Support_Center">
            <div class="card">
                <h2>🛠️ Comprehensive Support Center</h2>
                <p>Get help with Smart Park NCR anytime, anywhere</p>

                <div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 12px; margin: 16px 0;">
                    <div style="background: var(--dark-bg); padding: 16px; border-radius: 8px; text-align: center; cursor: pointer;" onclick="alert('Starting live chat...')">
                        <div style="font-size: 24px; color: var(--success); margin-bottom: 8px;">💬</div>
                        <p style="font-weight: 600;">Live Chat</p>
                        <p style="font-size: 12px; color: var(--text-muted);">Available 24/7</p>
                    </div>
                    <div style="background: var(--dark-bg); padding: 16px; border-radius: 8px; text-align: center; cursor: pointer;" onclick="alert('Calling support...')">
                        <div style="font-size: 24px; color: var(--info); margin-bottom: 8px;">📞</div>
                        <p style="font-weight: 600;">Call Support</p>
                        <p style="font-size: 12px; color: var(--text-muted);">+91-11-1234-5678</p>
                    </div>
                    <div style="background: var(--dark-bg); padding: 16px; border-radius: 8px; text-align: center; cursor: pointer;" onclick="alert('Opening email...')">
                        <div style="font-size: 24px; color: var(--warning); margin-bottom: 8px;">📧</div>
                        <p style="font-weight: 600;">Email Support</p>
                        <p style="font-size: 12px; color: var(--text-muted);">4hr response</p>
                    </div>
                    <div style="background: var(--dark-bg); padding: 16px; border-radius: 8px; text-align: center; cursor: pointer;" onclick="alert('Emergency support activated!')">
                        <div style="font-size: 24px; color: var(--danger); margin-bottom: 8px;">🚨</div>
                        <p style="font-weight: 600;">Emergency</p>
                        <p style="font-size: 12px; color: var(--text-muted);">Urgent issues</p>
                    </div>
                </div>
            </div>

            <div class="card">
                <h2>❓ Frequently Asked Questions</h2>
                <div class="scrollable">
                    <details style="margin-bottom: 12px;">
                        <summary style="cursor: pointer; padding: 8px; background: var(--dark-bg); border-radius: 8px; font-weight: 600;">How do I book a parking spot?</summary>
                        <div style="padding: 12px; color: var(--text-secondary);">
                            <p>1. Search for your destination</p>
                            <p>2. Select available parking spot</p>
                            <p>3. Choose date, time and vehicle</p>
                            <p>4. Make payment and confirm booking</p>
                        </div>
                    </details>
                    <details style="margin-bottom: 12px;">
                        <summary style="cursor: pointer; padding: 8px; background: var(--dark-bg); border-radius: 8px; font-weight: 600;">Can I cancel my booking?</summary>
                        <div style="padding: 12px; color: var(--text-secondary);">
                            <p>Yes, you can cancel bookings:</p>
                            <p>• 30+ minutes before: Full refund</p>
                            <p>• 15-30 minutes before: 50% refund</p>
                            <p>• Less than 15 minutes: No refund</p>
                        </div>
                    </details>
                    <details style="margin-bottom: 12px;">
                        <summary style="cursor: pointer; padding: 8px; background: var(--dark-bg); border-radius: 8px; font-weight: 600;">What payment methods are accepted?</summary>
                        <div style="padding: 12px; color: var(--text-secondary);">
                            <p>We accept:</p>
                            <p>• Smart Wallet (instant)</p>
                            <p>• UPI payments</p>
                            <p>• Credit/Debit cards</p>
                            <p>• Net banking</p>
                            <p>• Digital wallets</p>
                        </div>
                    </details>
                    <details style="margin-bottom: 12px;">
                        <summary style="cursor: pointer; padding: 8px; background: var(--dark-bg); border-radius: 8px; font-weight: 600;">How do I add a new vehicle?</summary>
                        <div style="padding: 12px; color: var(--text-secondary);">
                            <p>Go to Vehicle Management section and:</p>
                            <p>1. Click "Add New Vehicle"</p>
                            <p>2. Enter vehicle details</p>
                            <p>3. Upload required documents</p>
                            <p>4. Wait for verification (24-48 hours)</p>
                        </div>
                    </details>
                </div>
            </div>

            <div class="card">
                <h2>📝 Submit Feedback</h2>
                <textarea placeholder="Tell us about your experience or report an issue..."></textarea>
                <div style="display: flex; gap: 8px; margin: 12px 0;">
                    <button class="btn">📝 Send Feedback</button>
                    <button class="btn btn-danger">🐛 Report Bug</button>
                    <button class="btn">💡 Suggest Feature</button>
                </div>
            </div>
        </section>

    </main>
</div>

<script>
    // Tab switching functionality
    const tabButtons = document.querySelectorAll('.tab-btn');
    const sections = document.querySelectorAll('section');

    function switchTab(tabName) {
        // Remove active class from all buttons and sections
        tabButtons.forEach(btn => btn.classList.remove('active'));
        sections.forEach(sec => sec.classList.remove('active'));

        // Add active class to target button and section
        const targetBtn = document.querySelector(`[data-tab="${tabName}"]`);
        const targetSec = document.getElementById(tabName);

        if (targetBtn && targetSec) {
            targetBtn.classList.add('active');
            targetSec.classList.add('active');
        }
    }

    // Add click event listeners to all tab buttons
    tabButtons.forEach(button => {
        button.addEventListener('click', () => {
            const tabName = button.getAttribute('data-tab');
            switchTab(tabName);
        });
    });

    // Search parking functionality
    function searchParking(event) {
        event.preventDefault();
        const location = document.getElementById('search-location').value;
        const vehicle = document.getElementById('search-vehicle').value;
        const duration = document.getElementById('search-duration').value;

        alert(`🔍 Searching parking spots...\n\n📍 Location: ${location}\n🚗 Vehicle: ${vehicle}\n⏰ Duration: ${duration} hour(s)\n\n✅ Found 12 available spots nearby!`);
    }

    // Toggle setting functionality
    function toggleSetting(element) {
        element.classList.toggle('active');
        element.classList.toggle('off');

        const isActive = element.classList.contains('active');
        const settingName = element.previousElementSibling.textContent;

        alert(`${settingName}: ${isActive ? 'Enabled' : 'Disabled'}`);
    }

    // Filter functions
    function filterHistory(type) {
        alert(`Filtering booking history by: ${type}`);
    }

    function filterNotifications(type) {
        alert(`Filtering notifications by: ${type}`);
    }

    // Initialize app
    document.addEventListener('DOMContentLoaded', function() {
        console.log('🚗 Smart Park NCR Complete Single Page App Loaded');
        console.log('👤 Welcome, Vatsal Gupta!');

        // Simulate real-time updates
        setInterval(() => {
            // Update booking time remaining (simulation)
            const timeElements = document.querySelectorAll('[style*="color: var(--warning)"]');
            timeElements.forEach(el => {
                if (el.textContent.includes('h') && el.textContent.includes('m')) {
                    // Simulate countdown
                    console.log('⏰ Updating parking time...');
                }
            });
        }, 60000); // Update every minute
    });

    // Additional interactive functions
    function extendBooking() {
        if (confirm('Extend parking by 1 hour for ₹30?')) {
            alert('✅ Booking extended successfully!\nNew end time: 7:15 PM');
        }
    }

    function addMoney() {
        const amount = prompt('Enter amount to add to wallet:', '500');
        if (amount && amount > 0) {
            alert(`💰 Adding ₹${amount} to your wallet...\n✅ Payment successful!`);
        }
    }
</script>
</body>
</html>