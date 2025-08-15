<script>
  import FileUploader from '$lib/FileUploader.svelte';
  
  let selectedFiles = [];
  let zipCreated = false;
  let errorMessage = '';
  
  function handleFilesSelected(event) {
    selectedFiles = event.detail.files;
  }
  
  function handleZipCreated(event) {
    zipCreated = true;
    // Reset after 3 seconds
    setTimeout(() => {
      zipCreated = false;
    }, 3000);
  }
  
  function handleError(event) {
    errorMessage = event.detail.message;
    // Clear error after 5 seconds
    setTimeout(() => {
      errorMessage = '';
    }, 5000);
  }
</script>

<svelte:head>
  <title>File Uploader & ZIP Creator - LunexWeb</title>
  <meta name="description" content="Upload files with drag and drop, then download them as a ZIP file. Built with SvelteKit and JSZip.">
</svelte:head>

<div class="file-uploader-page">
  <div class="container mx-auto px-4 py-8">
    <!-- Header -->
    <div class="text-center mb-12">
      <h1 class="text-4xl font-bold text-gray-900 mb-4">File Uploader & ZIP Creator</h1>
      <p class="text-xl text-gray-600 max-w-3xl mx-auto">
        Drag and drop files to upload them, then download everything as a single ZIP file. 
        Perfect for organizing multiple files into one downloadable package.
      </p>
    </div>
    
    <!-- Success Message -->
    {#if zipCreated}
      <div class="success-message">
        <svg fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"></path>
        </svg>
        <span>ZIP file created and downloaded successfully!</span>
      </div>
    {/if}
    
    <!-- Error Message -->
    {#if errorMessage}
      <div class="error-message">
        <svg fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4m0 4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path>
        </svg>
        <span>{errorMessage}</span>
      </div>
    {/if}
    
    <!-- File Uploader Component -->
    <FileUploader 
      on:filesSelected={handleFilesSelected}
      on:zipCreated={handleZipCreated}
      on:error={handleError}
    />
    
    <!-- Features Section -->
    <div class="features-section mt-16">
      <h2 class="text-3xl font-bold text-gray-900 text-center mb-12">Features</h2>
      
      <div class="grid md:grid-cols-3 gap-8">
        <div class="feature-card">
          <div class="feature-icon">
            <svg fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12"></path>
            </svg>
          </div>
          <h3 class="text-xl font-semibold text-gray-900 mb-3">Drag & Drop</h3>
          <p class="text-gray-600">
            Simply drag files from your computer and drop them onto the upload area. 
            Supports multiple files at once.
          </p>
        </div>
        
        <div class="feature-card">
          <div class="feature-icon">
            <svg fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 10v6m0 0l-3-3m3 3l3-3m2 8H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path>
            </svg>
          </div>
          <h3 class="text-xl font-semibold text-gray-900 mb-3">ZIP Creation</h3>
          <p class="text-gray-600">
            Automatically creates a ZIP file containing all your uploaded files. 
            Download with a single click.
          </p>
        </div>
        
        <div class="feature-card">
          <div class="feature-icon">
            <svg fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"></path>
            </svg>
          </div>
          <h3 class="text-xl font-semibold text-gray-900 mb-3">Client-Side</h3>
          <p class="text-gray-600">
            All processing happens in your browser. No files are uploaded to our servers - 
            your privacy is protected.
          </p>
        </div>
      </div>
    </div>
    
    <!-- How It Works -->
    <div class="how-it-works mt-16">
      <h2 class="text-3xl font-bold text-gray-900 text-center mb-12">How It Works</h2>
      
      <div class="steps-container">
        <div class="step">
          <div class="step-number">1</div>
          <div class="step-content">
            <h3 class="text-lg font-semibold text-gray-900 mb-2">Upload Files</h3>
            <p class="text-gray-600">Drag and drop files or click to browse and select multiple files from your computer.</p>
          </div>
        </div>
        
        <div class="step">
          <div class="step-number">2</div>
          <div class="step-content">
            <h3 class="text-lg font-semibold text-gray-900 mb-2">Review & Organize</h3>
            <p class="text-gray-600">See all your files listed with names, sizes, and file types. Remove any files you don't want.</p>
          </div>
        </div>
        
        <div class="step">
          <div class="step-number">3</div>
          <div class="step-content">
            <h3 class="text-lg font-semibold text-gray-900 mb-2">Create ZIP</h3>
            <p class="text-gray-600">Click "Download as ZIP" to create and download a compressed file containing all your selected files.</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<style>
  .file-uploader-page {
    min-height: 100vh;
    background: linear-gradient(to bottom right, #eff6ff, #e0e7ff);
  }
  
  .success-message {
    background-color: #dcfce7;
    border: 1px solid #4ade80;
    color: #15803d;
    padding: 0.75rem 1rem;
    border-radius: 0.5rem;
    margin-bottom: 1.5rem;
    display: flex;
    align-items: center;
    gap: 0.5rem;
    max-width: 42rem;
    margin-left: auto;
    margin-right: auto;
  }
  
  .error-message {
    background-color: #fee2e2;
    border: 1px solid #f87171;
    color: #dc2626;
    padding: 0.75rem 1rem;
    border-radius: 0.5rem;
    margin-bottom: 1.5rem;
    display: flex;
    align-items: center;
    gap: 0.5rem;
    max-width: 42rem;
    margin-left: auto;
    margin-right: auto;
  }
  
  .features-section {
    background-color: white;
    border-radius: 1rem;
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
    padding: 2rem;
  }
  
  .feature-card {
    text-align: center;
    padding: 1.5rem;
    border-radius: 0.5rem;
    transition: background-color 0.2s;
  }
  
  .feature-card:hover {
    background-color: #f9fafb;
  }
  
  .feature-icon {
    width: 4rem;
    height: 4rem;
    background-color: #dbeafe;
    color: #2563eb;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0 auto 1rem auto;
  }
  
  .how-it-works {
    background-color: white;
    border-radius: 1rem;
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
    padding: 2rem;
  }
  
  .steps-container {
    display: flex;
    flex-direction: column;
    gap: 2rem;
  }
  
  .step {
    display: flex;
    align-items: flex-start;
    gap: 1.5rem;
  }
  
  .step-number {
    width: 3rem;
    height: 3rem;
    background-color: #2563eb;
    color: white;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.25rem;
    font-weight: bold;
    flex-shrink: 0;
  }
  
  .step-content {
    flex: 1;
  }
  
  @media (max-width: 768px) {
    .step {
      flex-direction: column;
      align-items: center;
      text-align: center;
      gap: 0;
    }
    
    .step > * + * {
      margin-top: 1rem;
    }
  }
</style> 