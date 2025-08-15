<script>
  import { onMount, createEventDispatcher } from 'svelte';
  import JSZip from 'jszip';
  
  const dispatch = createEventDispatcher();
  
  let dropZone;
  let fileInput;
  let isDragOver = false;
  let files = [];
  let isProcessing = false;
  let zipBlob = null;
  
  // Drag and drop event handlers
  function handleDragOver(e) {
    e.preventDefault();
    isDragOver = true;
  }
  
  function handleDragLeave(e) {
    e.preventDefault();
    isDragOver = false;
  }
  
  function handleDrop(e) {
    e.preventDefault();
    isDragOver = false;
    
    const droppedFiles = Array.from(e.dataTransfer.files);
    handleFiles(droppedFiles);
  }
  
  function handleFileSelect(e) {
    const selectedFiles = Array.from(e.target.files);
    handleFiles(selectedFiles);
  }
  
  function handleFiles(newFiles) {
    files = [...files, ...newFiles];
    dispatch('filesSelected', { files: files });
  }
  
  function removeFile(index) {
    files = files.filter((_, i) => i !== index);
    dispatch('filesSelected', { files: files });
  }
  
  async function createZip() {
    if (files.length === 0) return;
    
    isProcessing = true;
    
    try {
      const zip = new JSZip();
      
      // Add each file to the zip
      files.forEach((file, index) => {
        const fileName = file.name || `file_${index + 1}`;
        zip.file(fileName, file);
      });
      
      // Generate the zip file
      zipBlob = await zip.generateAsync({ type: 'blob' });
      
      // Create download link
      const url = URL.createObjectURL(zipBlob);
      const a = document.createElement('a');
      a.href = url;
      a.download = 'files.zip';
      document.body.appendChild(a);
      a.click();
      document.body.removeChild(a);
      URL.revokeObjectURL(url);
      
      dispatch('zipCreated', { zipBlob });
    } catch (error) {
      console.error('Error creating zip:', error);
      dispatch('error', { message: 'Failed to create zip file' });
    } finally {
      isProcessing = false;
    }
  }
  
  function clearFiles() {
    files = [];
    zipBlob = null;
    dispatch('filesSelected', { files: [] });
  }
</script>

<div class="file-uploader">
  <!-- Drop Zone -->
  <div
    bind:this={dropZone}
    class="drop-zone {isDragOver ? 'drag-over' : ''}"
    on:dragover={handleDragOver}
    on:dragleave={handleDragLeave}
    on:drop={handleDrop}
  >
    <div class="drop-content">
      <svg class="upload-icon" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12"></path>
      </svg>
      <h3 class="text-lg font-semibold text-gray-700 mb-2">Drop files here</h3>
      <p class="text-gray-500 mb-4">or click to browse</p>
      <button
        type="button"
        class="browse-btn"
        on:click={() => fileInput.click()}
      >
        Browse Files
      </button>
    </div>
    
    <!-- Hidden file input -->
    <input
      bind:this={fileInput}
      type="file"
      multiple
      class="hidden"
      on:change={handleFileSelect}
    />
  </div>
  
  <!-- File List -->
  {#if files.length > 0}
    <div class="file-list">
      <div class="file-list-header">
        <h4 class="text-lg font-semibold text-gray-700">Selected Files ({files.length})</h4>
        <button
          type="button"
          class="clear-btn"
          on:click={clearFiles}
        >
          Clear All
        </button>
      </div>
      
      <div class="files-grid">
        {#each files as file, index}
          <div class="file-item">
            <div class="file-info">
              <div class="file-icon">
                {#if file.type.startsWith('image/')}
                  <svg fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z"></path>
                  </svg>
                {:else if file.type.startsWith('video/')}
                  <svg fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 10l4.553-2.276A1 1 0 0121 8.618v6.764a1 1 0 01-1.447.894L15 14M5 18h8a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v8a2 2 0 002 2z"></path>
                  </svg>
                {:else}
                  <svg fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path>
                  </svg>
                {/if}
              </div>
              <div class="file-details">
                <p class="file-name">{file.name}</p>
                <p class="file-size">{(file.size / 1024 / 1024).toFixed(2)} MB</p>
              </div>
            </div>
            <button
              type="button"
              class="remove-btn"
              on:click={() => removeFile(index)}
            >
              <svg fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
              </svg>
            </button>
          </div>
        {/each}
      </div>
      
      <!-- Actions -->
      <div class="actions">
        <button
          type="button"
          class="zip-btn {isProcessing ? 'processing' : ''}"
          on:click={createZip}
          disabled={isProcessing}
        >
          {#if isProcessing}
            <svg class="animate-spin -ml-1 mr-3 h-5 w-5 text-white" fill="none" viewBox="0 0 24 24">
              <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
              <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
            </svg>
            Creating ZIP...
          {:else}
            <svg fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 10v6m0 0l-3-3m3 3l3-3m2 8H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path>
            </svg>
            Download as ZIP
          {/if}
        </button>
      </div>
    </div>
  {/if}
</div>

<style>
  .file-uploader {
    width: 100%;
    max-width: 64rem;
    margin-left: auto;
    margin-right: auto;
  }
  
  .drop-zone {
    border: 2px dashed #d1d5db;
    border-radius: 0.5rem;
    padding: 2rem;
    text-align: center;
    transition: all 0.2s;
    cursor: pointer;
  }
  
  .drop-zone:hover {
    border-color: #60a5fa;
    background-color: #eff6ff;
  }
  
  .drop-zone.drag-over {
    border-color: #3b82f6;
    background-color: #dbeafe;
    transform: scale(1.05);
  }
  
  .drop-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
  
  .upload-icon {
    width: 4rem;
    height: 4rem;
    color: #9ca3af;
    margin-bottom: 1rem;
  }
  
  .browse-btn {
    background-color: #2563eb;
    color: white;
    padding: 0.75rem 1.5rem;
    border-radius: 0.5rem;
    transition: background-color 0.2s;
    font-weight: 500;
    border: none;
    cursor: pointer;
  }
  
  .browse-btn:hover {
    background-color: #1d4ed8;
  }
  
  .file-list {
    margin-top: 2rem;
    background-color: white;
    border-radius: 0.5rem;
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
    padding: 1.5rem;
  }
  
  .file-list-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 1rem;
    padding-bottom: 1rem;
    border-bottom: 1px solid #e5e7eb;
  }
  
  .clear-btn {
    color: #dc2626;
    font-size: 0.875rem;
    font-weight: 500;
    transition: color 0.2s;
    background: none;
    border: none;
    cursor: pointer;
  }
  
  .clear-btn:hover {
    color: #b91c1c;
  }
  
  .files-grid {
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
    margin-bottom: 1.5rem;
  }
  
  .file-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 1rem;
    background-color: #f9fafb;
    border-radius: 0.5rem;
    transition: background-color 0.2s;
  }
  
  .file-item:hover {
    background-color: #f3f4f6;
  }
  
  .file-info {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    flex: 1;
  }
  
  .file-icon {
    width: 2.5rem;
    height: 2.5rem;
    color: #6b7280;
    flex-shrink: 0;
  }
  
  .file-details {
    flex: 1;
    min-width: 0;
  }
  
  .file-name {
    font-size: 0.875rem;
    font-weight: 500;
    color: #111827;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
  
  .file-size {
    font-size: 0.75rem;
    color: #6b7280;
  }
  
  .remove-btn {
    padding: 0.5rem;
    color: #9ca3af;
    transition: all 0.2s;
    border-radius: 50%;
    background: none;
    border: none;
    cursor: pointer;
  }
  
  .remove-btn:hover {
    color: #dc2626;
    background-color: #fef2f2;
  }
  
  .actions {
    display: flex;
    justify-content: center;
  }
  
  .zip-btn {
    background-color: #16a34a;
    color: white;
    padding: 0.75rem 2rem;
    border-radius: 0.5rem;
    transition: all 0.2s;
    font-weight: 500;
    display: flex;
    align-items: center;
    gap: 0.5rem;
    border: none;
    cursor: pointer;
  }
  
  .zip-btn:hover:not(:disabled) {
    background-color: #15803d;
  }
  
  .zip-btn:disabled {
    opacity: 0.5;
    cursor: not-allowed;
  }
  
  .zip-btn.processing {
    background-color: #15803d;
  }
  
  .hidden {
    display: none;
  }
</style> 