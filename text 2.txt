<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>YouTube Audio Uploader Simulator</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f7f9fb;
        }
        .container {
            max-width: 90%;
        }
        .upload-card {
            background-color: white;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.08);
        }
        .upload-btn {
            background-color: #ff0000;
            transition: background-color 0.2s, transform 0.1s;
        }
        .upload-btn:hover {
            background-color: #cc0000;
            transform: translateY(-1px);
        }
        .upload-btn:disabled {
            background-color: #e5e7eb;
            color: #9ca3af;
            cursor: not-allowed;
            transform: none;
        }
    </style>
</head>
<body class="flex items-center justify-center min-h-screen p-4 md:p-8">

    <div class="container w-full max-w-2xl">
        <header class="text-center mb-8">
            <h1 class="text-3xl font-extrabold text-gray-800">YouTube Audio Uploader (Simulated)</h1>
            <p class="text-gray-500 mt-2">Combine an MP3 file with a static image and simulate the upload to YouTube.</p>
        </header>

        <div id="upload-card" class="upload-card p-6 md:p-10 rounded-xl space-y-6">

            <!-- File Inputs -->
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                
                <!-- MP3 Input -->
                <div>
                    <label for="mp3File" class="block text-sm font-medium text-gray-700 mb-2 flex items-center">
                        <svg class="w-5 h-5 mr-1 text-red-500" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19V6l12-3v13M9 19c0 1.105-1.79 2-4 2s-4-.895-4-2 1.79-2 4-2 4 .895 4 2zm12-3c0 1.105-1.79 2-4 2s-4-.895-4-2 1.79-2 4-2 4 .895 4 2zM9 10l12-3"></path></svg>
                        1. Select MP3 Audio
                    </label>
                    <input type="file" id="mp3File" accept=".mp3" class="w-full text-sm text-gray-500 file:mr-4 file:py-2 file:px-4 file:rounded-lg file:border-0 file:text-sm file:font-semibold file:bg-red-50 file:text-red-700 hover:file:bg-red-100 transition duration-150 rounded-lg border border-gray-300 p-2.5">
                    <p class="text-xs text-gray-400 mt-1">Required: MP3 file format.</p>
                </div>

                <!-- Image Input -->
                <div>
                    <label for="imageFile" class="block text-sm font-medium text-gray-700 mb-2 flex items-center">
                        <svg class="w-5 h-5 mr-1 text-blue-500" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z"></path></svg>
                        2. Select Cover Image
                    </label>
                    <input type="file" id="imageFile" accept="image/*" class="w-full text-sm text-gray-500 file:mr-4 file:py-2 file:px-4 file:rounded-lg file:border-0 file:text-sm file:font-semibold file:bg-blue-50 file:text-blue-700 hover:file:bg-blue-100 transition duration-150 rounded-lg border border-gray-300 p-2.5">
                    <p class="text-xs text-gray-400 mt-1">Required: PNG or JPG file format (16:9 aspect ratio recommended).</p>
                </div>
            </div>

            <!-- Metadata Inputs -->
            <div class="space-y-4 pt-4">
                <div>
                    <label for="videoTitle" class="block text-sm font-medium text-gray-700 mb-2">3. Video Title</label>
                    <input type="text" id="videoTitle" placeholder="My Awesome New Track (Official Audio)" class="w-full border border-gray-300 rounded-lg p-3 focus:ring-red-500 focus:border-red-500" maxlength="100">
                </div>
                <div>
                    <label for="videoDescription" class="block text-sm font-medium text-gray-700 mb-2">4. Video Description</label>
                    <textarea id="videoDescription" rows="4" placeholder="Description, links, and track details go here..." class="w-full border border-gray-300 rounded-lg p-3 focus:ring-red-500 focus:border-red-500"></textarea>
                </div>
            </div>
            
            <!-- Upload Button -->
            <button id="uploadButton" onclick="simulateUpload()" disabled class="upload-btn w-full py-3 rounded-xl text-white font-bold text-lg shadow-lg shadow-red-500/50 flex items-center justify-center">
                <svg id="uploadIcon" class="w-6 h-6 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-8l-4-4m0 0L8 8m4-4v12"></path></svg>
                <div id="buttonText">Start Simulated Upload to YouTube</div>
                <svg id="spinner" class="animate-spin -ml-1 mr-3 h-5 w-5 text-white hidden" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                    <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                    <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                </svg>
            </button>

            <!-- Status Log -->
            <div id="statusLog" class="pt-4 space-y-2 text-sm text-gray-600 bg-gray-50 p-4 rounded-lg border border-gray-200 hidden">
                <p class="font-semibold text-gray-800">Processing Status:</p>
            </div>
            
        </div>

        <!-- Warning Box -->
        <div class="mt-8 p-4 bg-yellow-100 border-l-4 border-yellow-500 text-yellow-800 rounded-lg" role="alert">
            <p class="font-bold">Backend Simulation Notice</p>
            <p class="text-sm">Since this app runs purely in your browser, the **video conversion** (MP3 + Image -> MP4) and the **final YouTube upload** are simulated using timed delays and console logging. This showcases the workflow but does not actually upload anything.</p>
        </div>

    </div>

    <script>
        // --- Core Application Logic ---

        const mp3File = document.getElementById('mp3File');
        const imageFile = document.getElementById('imageFile');
        const uploadButton = document.getElementById('uploadButton');
        const buttonText = document.getElementById('buttonText');
        const spinner = document.getElementById('spinner');
        const uploadIcon = document.getElementById('uploadIcon');
        const statusLog = document.getElementById('statusLog');
        const videoTitle = document.getElementById('videoTitle');
        const videoDescription = document.getElementById('videoDescription');

        /**
         * Checks if required files are selected and enables/disables the upload button.
         */
        function checkInputs() {
            const isReady = mp3File.files.length > 0 && imageFile.files.length > 0 && videoTitle.value.trim() !== "";
            uploadButton.disabled = !isReady;
        }

        // Attach listeners to check input state
        mp3File.addEventListener('change', checkInputs);
        imageFile.addEventListener('change', checkInputs);
        videoTitle.addEventListener('input', checkInputs);


        /**
         * Utility function to log status messages to the UI.
         * @param {string} message The message to display.
         * @param {string} color Tailwind color class for the dot.
         */
        function logStatus(message, color = 'text-gray-500') {
            statusLog.classList.remove('hidden');
            const logItem = document.createElement('p');
            logItem.classList.add('flex', 'items-center');
            
            const dot = document.createElement('span');
            dot.classList.add('w-2', 'h-2', 'rounded-full', 'inline-block', 'mr-2', 'flex-shrink-0');
            dot.classList.add(color);
            dot.style.backgroundColor = color.includes('red') ? '#ef4444' : (color.includes('blue') ? '#3b82f6' : '#6b7280'); // Fallback colors

            logItem.innerHTML = `<span class="${color.replace('text-', 'bg-')} w-2 h-2 rounded-full inline-block mr-2 flex-shrink-0"></span> ${message}`;
            statusLog.appendChild(logItem);
            statusLog.scrollTop = statusLog.scrollHeight; // Scroll to bottom
        }

        /**
         * Simulates the multi-step upload process.
         */
        async function simulateUpload() {
            // 1. Reset UI State
            uploadButton.disabled = true;
            spinner.classList.remove('hidden');
            uploadIcon.classList.add('hidden');
            buttonText.textContent = 'Processing...';
            statusLog.innerHTML = '<p class="font-semibold text-gray-800">Processing Status:</p>';
            statusLog.classList.remove('hidden');

            const mp3 = mp3File.files[0];
            const image = imageFile.files[0];
            const title = videoTitle.value.trim();
            const description = videoDescription.value.trim();

            console.log("--- STARTING SIMULATION ---");
            console.log(`MP3 File: ${mp3.name} (${(mp3.size / 1024 / 1024).toFixed(2)} MB)`);
            console.log(`Image File: ${image.name} (${(image.size / 1024 / 1024).toFixed(2)} MB)`);
            console.log(`Video Title: ${title}`);
            console.log(`Video Description: ${description}`);
            
            try {
                // Step 1: Client-side file selection and basic validation
                logStatus(`[Step 1/5] Files accepted by client (Title: "${title}").`, 'text-green-500');
                await new Promise(r => setTimeout(r, 500));

                // Step 2: Simulated Server Upload
                logStatus(`[Step 2/5] Uploading files to simulated server... (5s delay)`, 'text-yellow-600');
                console.log("SIMULATION: In a real app, files are now being uploaded to the backend server.");
                await new Promise(r => setTimeout(r, 5000));
                logStatus(`[Step 2/5] Files successfully received by server.`, 'text-green-500');
                
                // Step 3: Simulated Video Conversion (FFmpeg equivalent)
                logStatus(`[Step 3/5] Server starting video conversion (MP3 + Image -> MP4)... (8s delay)`, 'text-yellow-600');
                console.log("SIMULATION: Server is running FFmpeg command to merge audio and image into a single video file.");
                await new Promise(r => setTimeout(r, 8000));
                
                const fakeVideoId = "ABCDEFG" + Math.floor(Math.random() * 999);
                logStatus(`[Step 3/5] Conversion complete! Generated MP4 video file: ${fakeVideoId}.mp4`, 'text-green-500');

                // Step 4: Simulated YouTube API Authentication
                logStatus(`[Step 4/5] Initiating YouTube OAuth 2.0 flow and token exchange... (2s delay)`, 'text-yellow-600');
                console.log("SIMULATION: User must grant permission via the YouTube API to upload the video to their channel.");
                await new Promise(r => setTimeout(r, 2000));
                logStatus(`[Step 4/5] Authentication successful. Ready to insert video.`, 'text-green-500');

                // Step 5: Simulated YouTube Video Upload via Data API
                logStatus(`[Step 5/5] Calling YouTube Data API (videos.insert) with generated video file... (6s delay)`, 'text-yellow-600');
                console.log(`SIMULATION: Posting the video data via a resumable upload session for YouTube Video ID: ${fakeVideoId}`);
                await new Promise(r => setTimeout(r, 6000));

                logStatus(`[SUCCESS] Upload complete! Video is now processing on YouTube.`, 'text-red-600');
                logStatus(`[SUCCESS] Simulated YouTube Video ID: ${fakeVideoId}`, 'text-red-600');
                console.log(`--- SIMULATION SUCCESSFUL ---`);


            } catch (error) {
                logStatus(`[ERROR] An error occurred during simulation: ${error.message}`, 'text-red-500');
                console.error("Simulation Error:", error);
            } finally {
                // 3. Restore UI state
                spinner.classList.add('hidden');
                uploadIcon.classList.remove('hidden');
                buttonText.textContent = 'Upload Again';
                uploadButton.disabled = false;
            }
        }
    </script>
</body>
</html>

