# Object-Detection-and-Tracking_Rohan_Subhash_Jagtap

##HTML##

<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Meta tags for proper character encoding and responsive design -->
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <!-- Page Title -->
    <title>Object Detection & Tracking</title>
    
    <!-- Font Awesome for icons -->
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">

    <!-- Internal CSS Styles -->
    <style>
        /* Global Reset and Box-Sizing */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        /* Body Styling */
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
        }

        /* Container for full content */
        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }

        /* Header Styling */
        header {
            text-align: center;
            margin-bottom: 30px;
            color: white;
        }

        header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        header p {
            font-size: 1.1rem;
            opacity: 0.9;
        }

        /* Layout: Control panel + Video section */
        .main-content {
            display: grid;
            grid-template-columns: 300px 1fr;
            gap: 20px;
            align-items: start;
        }

        /* Left-side Control Panel */
        .control-panel {
            background: white;
            border-radius: 15px;
            padding: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            height: fit-content;
        }

        /* Section Styling in Control Panel */
        .section {
            margin-bottom: 25px;
        }

        .section h2, .section h3 {
            color: #4a5568;
            margin-bottom: 15px;
            font-size: 1.3rem;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .control-group {
            display: flex;
            flex-direction: column;
            gap: 10px;
            margin-bottom: 15px;
        }

        /* Button Base Styling */
        .btn {
            padding: 12px 20px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 14px;
            font-weight: 600;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            text-decoration: none;
        }

        /* Button Variants */
        .btn-primary { background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: white; }
        .btn-secondary { background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%); color: white; }
        .btn-success { background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%); color: white; }
        .btn-danger { background: linear-gradient(135deg, #fa709a 0%, #fee140 100%); color: white; }
        .btn-info { background: linear-gradient(135deg, #a8edea 0%, #fed6e3 100%); color: #333; }

        /* Hover effects for buttons */
        .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4); }
        .btn-secondary:hover { transform: translateY(-2px); box-shadow: 0 5px 15px rgba(245, 87, 108, 0.4); }
        .btn-success:hover { transform: translateY(-2px); box-shadow: 0 5px 15px rgba(79, 172, 254, 0.4); }
        .btn-danger:hover { transform: translateY(-2px); box-shadow: 0 5px 15px rgba(250, 112, 154, 0.4); }
        .btn-info:hover { transform: translateY(-2px); box-shadow: 0 5px 15px rgba(168, 237, 234, 0.4); }

        /* Disabled button state */
        .btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none !important;
            box-shadow: none !important;
        }

        /* Settings Input Group Styling */
        .setting-group {
            margin-bottom: 15px;
        }
        .setting-group label { display: block; margin-bottom: 5px; font-weight: 500; color: #4a5568; }
        .setting-group input[type="range"] { width: 100%; margin-bottom: 5px; }
        .setting-group select { width: 100%; padding: 8px; border: 2px solid #e2e8f0; border-radius: 6px; font-size: 14px; }

        /* Video Section Styling */
        .video-section {
            background: white;
            border-radius: 15px;
            padding: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }

        /* Video Player Container */
        .video-container {
            position: relative;
            width: 100%;
            height: 480px;
            background: #000;
            border-radius: 10px;
            overflow: hidden;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        /* Video Placeholder shown before video loads */
        .video-placeholder {
            text-align: center;
            color: white;
        }

        /* Actual Video Stream */
        #video-stream {
            width: 100%;
            height: 100%;
            object-fit: contain;
        }

        /* Overlay for FPS counter & Status */
        .video-overlay {
            position: absolute;
            top: 10px;
            left: 10px;
            right: 10px;
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            pointer-events: none;
        }

        /* FPS Counter Display */
        .fps-counter {
            background: rgba(0,0,0,0.7);
            color: white;
            padding: 5px 10px;
            border-radius: 5px;
            font-family: monospace;
            font-size: 14px;
        }

        /* Status Indicator */
        .status-indicator {
            background: rgba(0,0,0,0.7);
            color: white;
            padding: 5px 10px;
            border-radius: 5px;
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 14px;
        }

        /* Status Dot (green blinking) */
        .status-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: #10b981;
            animation: pulse 2s infinite;
        }

        /* Animation for blinking status */
        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }

        /* Responsive design for smaller screens */
        @media (max-width: 768px) {
            .main-content { grid-template-columns: 1fr; }
            .container { padding: 10px; }
            header h1 { font-size: 2rem; }
            .video-container { height: 300px; }
        }
    </style>
</head>
<body>
    <!-- Main Container -->
    <div class="container">

        <!-- Page Header -->
        <header>
            <h1><i class="fas fa-eye"></i> Object Detection & Tracking</h1>
            <p>Real-time object detection and tracking using YOLO and DeepSORT</p>
        </header>

        <!-- Main Grid Layout: Control Panel (Left) + Video Section (Right) -->
        <div class="main-content">

            <!-- Control Panel (Left Sidebar) -->
            <div class="control-panel">
                <div class="section">
                    <h2><i class="fas fa-cog"></i> Controls</h2>
                    
                    <!-- Control Group: Start/Stop and Upload Video -->
                    <div class="control-group">
                        <!-- Start Webcam Button -->
                        <button class="btn btn-primary" id="webcam-btn">
                            <i class="fas fa-video"></i> Start Webcam
                        </button>
                        
                        <!-- Upload Video Button (hidden file input) -->
                        <div class="file-input-group">
                            <input type="file" id="video-file" accept="video/*" hidden>
                            <button class="btn btn-secondary" onclick="document.getElementById('video-file').click()">
                                <i class="fas fa-file-video"></i> Upload Video
                            </button>
                        </div>
                        
                        <!-- Stop Button (disabled by default) -->
                        <button class="btn btn-danger" id="stop-btn" disabled>
                            <i class="fas fa-stop"></i> Stop
                        </button>
                    </div>
                    
                    <!-- Control Group: Capture and Stats -->
                    <div class="control-group">
                        <!-- Capture Frame Button -->
                        <button class="btn btn-success" id="capture-btn" disabled>
                            <i class="fas fa-camera"></i> Capture Frame
                        </button>
                        
                        <!-- Statistics Button -->
                        <button class="btn btn-info" id="stats-btn">
                            <!-- Icon and Label will go here -->
