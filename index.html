<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Gestión de Tickets</title>

  <!-- Bootstrap 5 -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet" />

  <!-- FontAwesome -->
  <script src="https://kit.fontawesome.com/a2b5d5d15e.js" crossorigin="anonymous"></script>

  <!-- SweetAlert2 -->
  <script src="https://cdn.jsdelivr.net/npm/sweetalert2@11"></script>

  <!-- Chart.js -->
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

  <!-- jsPDF -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>

  <style>
    body {
      background-color: #f8f9fa;
    }
    .hidden {
      display: none;
    }
  </style>
</head>
<body>
  <div class="container py-5">
    <!-- LOGIN / REGISTRO -->
    <div id="authSection">
      <h2 class="text-center mb-4">Iniciar Sesión</h2>
      <div class="mb-3">
        <input type="email" id="email" class="form-control" placeholder="Correo electrónico" />
      </div>
      <div class="mb-3">
        <input type="password" id="password" class="form-control" placeholder="Contraseña" />
      </div>
      <div class="d-flex justify-content-between mb-3">
        <button class="btn btn-primary" onclick="login()">Ingresar</button>
        <button class="btn btn-secondary" onclick="register()">Registrarse</button>
      </div>
      <div class="text-center">
        <a href="#" onclick="resetPassword()">¿Olvidaste tu contraseña?</a>
      </div>
    </div>

    <!-- DASHBOARD -->
    <div id="dashboardSection" class="hidden">
      <h2>Bienvenido, <span id="userEmail"></span></h2>
      <div class="d-flex justify-content-between my-4">
        <button class="btn btn-success" onclick="showTicketForm()">Crear Ticket</button>
        <button class="btn btn-outline-danger" onclick="exportCSV()">Exportar CSV</button>
      </div>

      <!-- Gráfico -->
      <canvas id="priorityChart" height="100"></canvas>

      <!-- Formulario de creación de ticket -->
      <div id="ticketForm" class="my-4 hidden">
        <h4>Nuevo Ticket</h4>
        <div class="mb-2">
          <input type="text" id="titulo" class="form-control" placeholder="Título del ticket" />
        </div>
        <div class="mb-2">
          <textarea id="descripcion" class="form-control" placeholder="Descripción"></textarea>
        </div>
        <div class="mb-2">
          <select id="prioridad" class="form-select">
            <option value="">Prioridad</option>
            <option value="Alta">Alta</option>
            <option value="Media">Media</option>
            <option value="Baja">Baja</option>
          </select>
        </div>
        <div class="mb-2">
          <input type="text" id="tipo" class="form-control" placeholder="Tipo de pedido (ej. Empaque)" />
        </div>
        <button class="btn btn-primary" onclick="crearTicket()">Guardar Ticket</button>
      </div>

      <!-- Lista de tickets -->
      <div id="ticketList" class="mt-4"></div>
    </div>
  </div>

  <!-- Firebase SDK -->
  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.0/firebase-app.js";
    import {
      getAuth,
      createUserWithEmailAndPassword,
      signInWithEmailAndPassword,
      sendPasswordResetEmail,
      onAuthStateChanged,
      signOut
    } from "https://www.gstatic.com/firebasejs/11.6.0/firebase-auth.js";
    import {
      getFirestore,
      collection,
      addDoc,
      getDocs
    } from "https://www.gstatic.com/firebasejs/11.6.0/firebase-firestore.js";

    // Configuración Firebase
    const firebaseConfig = {
      apiKey: "AIzaSyDaLGTKTJ4l716_WNi84etNAozG9wp69M8",
      authDomain: "plataformaproqro.firebaseapp.com",
      projectId: "plataformaproqro",
      storageBucket: "plataformaproqro.appspot.com",
      messagingSenderId: "143130694419",
      appId: "1:143130694419:web:dd0465044ee881fdc5c0e6"
    };

    const app = initializeApp(firebaseConfig);
    const auth = getAuth(app);
    const db = getFirestore(app);

    // Elementos
    const authSection = document.getElementById("authSection");
    const dashboardSection = document.getElementById("dashboardSection");
    const userEmailSpan = document.getElementById("userEmail");

    // Funciones de autenticación
    window.login = async function () {
      const email = document.getElementById("email").value;
      const password = document.getElementById("password").value;
      try {
        await signInWithEmailAndPassword(auth, email, password);
        Swal.fire("¡Listo!", "Sesión iniciada con éxito", "success");
      } catch (e) {
        Swal.fire("Error", e.message, "error");
      }
    };

    window.register = async function () {
      const email = document.getElementById("email").value;
      const password = document.getElementById("password").value;
      try {
        await createUserWithEmailAndPassword(auth, email, password);
        Swal.fire("¡Registrado!", "Usuario creado correctamente", "success");
      } catch (e) {
        Swal.fire("Error", e.message, "error");
      }
    };

    window.resetPassword = async function () {
      const email = document.getElementById("email").value;
      if (!email) return Swal.fire("Aviso", "Ingresa tu correo", "info");
      await sendPasswordResetEmail(auth, email);
      Swal.fire("Revisa tu correo", "Enlace enviado", "success");
    };

    // Cambio de estado de sesión
    onAuthStateChanged(auth, (user) => {
      if (user) {
        authSection.classList.add("hidden");
        dashboardSection.classList.remove("hidden");
        userEmailSpan.textContent = user.email;
        cargarTickets();
        graficar();
      } else {
        authSection.classList.remove("hidden");
        dashboardSection.classList.add("hidden");
      }
    });

    // Mostrar formulario
    window.showTicketForm = () => {
      document.getElementById("ticketForm").classList.toggle("hidden");
    };

    // Crear ticket
    window.crearTicket = async () => {
      const titulo = document.getElementById("titulo").value;
      const descripcion = document.getElementById("descripcion").value;
      const prioridad = document.getElementById("prioridad").value;
      const tipo = document.getElementById("tipo").value;
      const fecha = new Date().toISOString();
      const folio = `TICKET-${Date.now()}`;

      try {
        await addDoc(collection(db, "tickets"), {
          titulo, descripcion, prioridad, tipo, fecha, folio, usuario: auth.currentUser.email
        });
        Swal.fire("¡Guardado!", "El ticket fue creado correctamente", "success");
        document.getElementById("ticketForm").reset();
        cargarTickets();
        graficar();
      } catch (e) {
        Swal.fire("Error", e.message, "error");
      }
    };

    // Cargar tickets
    async function cargarTickets() {
      const querySnapshot = await getDocs(collection(db, "tickets"));
      const lista = document.getElementById("ticketList");
      lista.innerHTML = "";
      querySnapshot.forEach((doc) => {
        const t = doc.data();
        const card = `
          <div class="card mb-3">
            <div class="card-body">
              <h5 class="card-title">${t.titulo}</h5>
              <p class="card-text">${t.descripcion}</p>
              <p><strong>Prioridad:</strong> ${t.prioridad} | <strong>Tipo:</strong> ${t.tipo}</p>
              <p><strong>Folio:</strong> ${t.folio}</p>
              <button class="btn btn-outline-secondary btn-sm" onclick='exportarPDF(${JSON.stringify(t)})'>
                <i class="fas fa-file-pdf"></i> Exportar PDF
              </button>
            </div>
          </div>`;
        lista.innerHTML += card;
      });
    }

    // Graficar prioridad
    async function graficar() {
      const querySnapshot = await getDocs(collection(db, "tickets"));
      let altas = 0, medias = 0, bajas = 0;
      querySnapshot.forEach((doc) => {
        const p = doc.data().prioridad;
        if (p === "Alta") altas++;
        else if (p === "Media") medias++;
        else if (p === "Baja") bajas++;
      });

      const ctx = document.getElementById("priorityChart").getContext("2d");
      new Chart(ctx, {
        type: "bar",
        data: {
          labels: ["Alta", "Media", "Baja"],
          datasets: [{
            label: "Tickets por Prioridad",
            data: [altas, medias, bajas],
            backgroundColor: ["#dc3545", "#ffc107", "#198754"]
          }]
        }
      });
    }

    // Exportar todos a CSV (básico)
    window.exportCSV = async () => {
      const querySnapshot = await getDocs(collection(db, "tickets"));
      let csv = "Folio,Titulo,Descripción,Prioridad,Tipo,Fecha,Usuario\n";
      querySnapshot.forEach((doc) => {
        const t = doc.data();
        csv += `${t.folio},"${t.titulo}","${t.descripcion}",${t.prioridad},${t.tipo},${t.fecha},${t.usuario}\n`;
      });
      const blob = new Blob([csv], { type: "text/csv;charset=utf-8;" });
      const link = document.createElement("a");
      link.href = URL.createObjectURL(blob);
      link.download = "tickets.csv";
      link.click();
    };

    // Exportar PDF individual
    window.exportarPDF = (ticket) => {
      const { jsPDF } = window.jspdf;
      const doc = new jsPDF();
      doc.text(`Folio: ${ticket.folio}`, 10, 10);
      doc.text(`Título: ${ticket.titulo}`, 10, 20);
      doc.text(`Descripción: ${ticket.descripcion}`, 10, 30);
      doc.text(`Prioridad: ${ticket.prioridad}`, 10, 40);
      doc.text(`Tipo: ${ticket.tipo}`, 10, 50);
      doc.text(`Fecha: ${ticket.fecha}`, 10, 60);
      doc.text(`Usuario: ${ticket.usuario}`, 10, 70);
      doc.save(`${ticket.folio}.pdf`);
    };
  </script>
</body>
</html>
