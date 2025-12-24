<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Future Baby Face Generator 👶✨</title>
    <style>
        body { font-family: 'Segoe UI', sans-serif; background: linear-gradient(135deg, #ffd1dc, #a0e7e5); color: #333; text-align: center; padding: 20px; min-height: 100vh; }
        h1 { font-size: 2.5em; margin: 20px 0; color: #fff; text-shadow: 2px 2px 10px rgba(0,0,0,0.3); }
        p { font-size: 1.2em; max-width: 800px; margin: 0 auto 30px; color: #fff; }
        .container { max-width: 900px; margin: 0 auto; background: rgba(255,255,255,0.9); border-radius: 20px; padding: 40px; box-shadow: 0 10px 30px rgba(0,0,0,0.2); }
        .uploads { display: grid; grid-template-columns: 1fr 1fr; gap: 30px; margin: 30px 0; }
        .upload-area { border: 3px dashed #ff69b4; border-radius: 15px; padding: 30px; background: #fff; }
        .upload-area:hover { border-color: #ff1493; }
        input[type="file"] { display: none; }
        label { cursor: pointer; font-size: 1.4em; color: #ff69b4; }
        #preview1, #preview2 { max-width: 250px; border-radius: 15px; margin: 15px 0; box-shadow: 0 5px 15px rgba(0,0,0,0.2); }
        .gender { margin: 30px 0; }
        .gender button { background: #fff; border: 3px solid #ff69b4; padding: 15px 30px; margin: 0 15px; border-radius: 50px; font-size: 1.2em; cursor: pointer; }
        .gender button.selected { background: #ff69b4; color: white; }
        button#generate { background: #ff69b4; color: white; border: none; padding: 18px 40px; font-size: 1.4em; border-radius: 50px; cursor: pointer; margin: 30px; transition: 0.3s; }
        button#generate:hover { background: #ff1493; transform: scale(1.05); }
        #result { margin: 50px 0; display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; align-items: center; }
        #result img { max-width: 100%; border-radius: 20px; box-shadow: 0 10px 30px rgba(0,0,0,0.3); }
        #caption { font-size: 1.6em; font-weight: bold; color: #ff69b4; grid-column: span 3; }
        footer { margin-top: 50px; color: #fff; font-size: 0.9em; }
        @media (max-width: 768px) { .uploads, #result { grid-template-columns: 1fr; } }
    </style>
</head>
<body>
    <h1>Future Baby Face Generator 👶✨</h1>
    <p>Upload photos of two parents (or you + a celeb!) and see your adorable future baby. Boy or girl? You choose!</p>
    
    <div class="container">
        <div class="uploads">
            <div class="upload-area">
                <label for="upload1">👩 Parent 1 Photo</label>
                <input type="file" id="upload1" accept="image/*">
                <img id="preview1" src="" alt="Parent 1">
            </div>
            <div class="upload-area">
                <label for="upload2">👨 Parent 2 Photo</label>
                <input type="file" id="upload2" accept="image/*">
                <img id="preview2" src="" alt="Parent 2">
            </div>
        </div>
        
        <div class="gender">
            <button class="selected" data-gender="boy">👦 Boy</button>
            <button data-gender="girl">👧 Girl</button>
        </div>
        
        <button id="generate">Generate My Baby! 🚀</button>
        
        <div id="result"></div>
    </div>
    
    <footer>Share your cute baby results! #FutureBabyGenerator 🎉</footer>

    <script>
        const upload1 = document.getElementById('upload1');
        const upload2 = document.getElementById('upload2');
        const preview1 = document.getElementById('preview1');
        const preview2 = document.getElementById('preview2');
        const genderBtns = document.querySelectorAll('.gender button');
        const generate = document.getElementById('generate');
        const result = document.getElementById('result');
        
        let parent1Image = '';
        let parent2Image = '';
        let selectedGender = 'boy';
        
        upload1.addEventListener('change', (e) => updatePreview(e, preview1, 'parent1Image'));
        upload2.addEventListener('change', (e) => updatePreview(e, preview2, 'parent2Image'));
        
        function updatePreview(e, previewEl, varName) {
            const file = e.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = (ev) => {
                    previewEl.src = ev.target.result;
                    previewEl.style.display = 'block';
                    window[varName] = ev.target.result;
                };
                reader.readAsDataURL(file);
            }
        }
        
        genderBtns.forEach(btn => {
            btn.addEventListener('click', () => {
                genderBtns.forEach(b => b.classList.remove('selected'));
                btn.classList.add('selected');
                selectedGender = btn.dataset.gender;
            });
        });
        
        generate.addEventListener('click', () => {
            if (!parent1Image || !parent2Image) {
                alert('Upload both parent photos first! 😊');
                return;
            }
            
            result.innerHTML = `
                <div><p><strong>Parent 1</strong></p><img src="${parent1Image}" alt="Parent 1"></div>
                <div><p><strong>Parent 2</strong></p><img src="${parent2Image}" alt="Parent 2"></div>
                <div><p><strong>Your Future Baby (${selectedGender === 'boy' ? 'Boy' : 'Girl'})!</strong></p>
                    <img src="https://via.placeholder.com/600x800/fff0f5/ff69b4?text=Adorable+AI+Baby+${selectedGender === 'boy' ? 'Boy' : 'Girl'}+Here!" alt="Baby Result">
                </div>
                <p id="caption">OMG this baby is too cute! 👶✨ Share your prediction!</p>
            `;
            
            // REAL AI TIP: Connect to Replicate/Hugging Face face-merge + baby-style models.
        });
    </script>
</body>
</html>
