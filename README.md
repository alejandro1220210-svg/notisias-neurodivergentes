<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import {
    getFirestore,
    collection,
    addDoc,
    onSnapshot,
    query,
    orderBy,
    serverTimestamp
  } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-firestore.js";

  // ✅ PON AQUÍ TUS CREDENCIALES REALES DE FIREBASE
  const firebaseConfig = {
    apiKey: "TU_API_KEY",
    authDomain: "TU_PROJECT_ID.firebaseapp.com",
    projectId: "TU_PROJECT_ID",
    storageBucket: "TU_PROJECT_ID.appspot.com",
    messagingSenderId: "TU_SENDER_ID",
    appId: "TU_APP_ID"
  };

  const app = initializeApp(firebaseConfig);
  const db = getFirestore(app);

  window.articles = [];
  window.activeCategory = 'Todas';
  window.searchQuery = '';

  // ✅ Todos los navegadores conectados ven las noticias en vivo
  const q = query(collection(db, "noticias"), orderBy("createdAt", "desc"));

  onSnapshot(q, (snapshot) => {
    window.articles = snapshot.docs.map(doc => ({
      id: doc.id,
      ...doc.data()
    }));

    renderCategoryNav();
    renderNews();
  });

  window.handlePublishArticle = async function (e) {
    e.preventDefault();

    const submitBtn = document.getElementById('submitBtn');
    submitBtn.disabled = true;
    submitBtn.innerText = "Guardando...";

    const title = document.getElementById('postTitle').value.trim();
    const category = document.getElementById('postCategory').value;
    const author = document.getElementById('postAuthor').value.trim();
    const imageInput = document.getElementById('postImage').value.trim();
    const summary = document.getElementById('postSummary').value.trim();
    const content = document.getElementById('postContent').value.trim();
    const isBreaking = document.getElementById('postIsBreaking').checked;

    const defaultImg = 'https://images.unsplash.com/photo-1504711434969-e33886168f5c?q=80&w=1000&auto=format&fit=crop';

    try {
      await addDoc(collection(db, "noticias"), {
        title,
        category,
        author,
        summary,
        content,
        image: imageInput !== '' ? imageInput : defaultImg,
        isBreaking,
        views: 1,
        createdAt: serverTimestamp()
      });

      closePublishModal();
      showToast('¡Noticia publicada y visible para todos!');
    } catch (err) {
      console.error("Error al guardar:", err);
      alert("Error al conectar con Firebase. Revisa la configuración.");
    } finally {
      submitBtn.disabled = false;
      submitBtn.innerHTML = `
        <i data-lucide="check" class="w-4 h-4"></i> Publicar para Todos
      `;
      lucide.createIcons();
    }
  };
</script>
