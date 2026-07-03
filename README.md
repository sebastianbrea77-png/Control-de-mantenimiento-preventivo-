# Control-de-mantenimiento-preventivo-
PowerMech Pro
```react
import React, { useState, useEffect } from 'react';

// --- ICONOS INLINE SVG ---
const Icons = {
  Dashboard: () => (
    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" strokeWidth={1.5} stroke="currentColor" className="w-5 h-5">
      <path strokeLinecap="round" strokeLinejoin="round" d="M2.25 13.5h3.86a2.25 2.25 0 012.008 1.24l.885 1.77a2.25 2.25 0 002.007 1.24h1.98a2.25 2.25 0 002.007-1.24l.885-1.77a2.25 2.25 0 012.007-1.24h3.86m-18 0h18a2.25 2.25 0 012.25 2.25v4.5A2.25 2.25 0 0118 22.5H6a2.25 2.25 0 01-2.25-2.25v-4.5m18-6.75a2.25 2.25 0 00-2.25-2.25H18A2.25 2.25 0 0015.75 9h-7.5A2.25 2.25 0 006 6.75H2.25m18 0V4.5A2.25 2.25 0 0018 2.25H6a2.25 2.25 0 00-2.25 2.25V6.75m18 0A2.25 2.25 0 0118 9H6A2.25 2.25 0 013.75 6.75" />
    </svg>
  ),
  Equipos: () => (
    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" strokeWidth={1.5} stroke="currentColor" className="w-5 h-5">
      <path strokeLinecap="round" strokeLinejoin="round" d="M11.42 15.17L17.25 21A1.5 1.5 0 0019.5 21l2.5-2.5a1.5 1.5 0 000-2.12l-5.83-5.83m-4.75 4.62l3.43-3.43m-3.43 3.43L6.75 21a1.5 1.5 0 01-2.25 0L2 18.5a1.5 1.5 0 010-2.12l5.83-5.83m.75 4.62l-3.43-3.43m3.43 3.43l3.43-3.43m-3.43 3.43L11.4 9.17m-3.1 3.1c-.18.18-.45.18-.63 0l-1.42-1.42a.45.45 0 010-.63l1.42-1.42a.45.45 0 01.63 0l1.42 1.42c.18.18.18.45 0 .63l-1.42 1.42zm7.1-7.1c-.18.18-.45.18-.63 0l-1.42-1.42a.45.45 0 010-.63l1.42-1.42a.45.45 0 01.63 0l1.42 1.42c.18.18.18.45 0 .63l-1.42 1.42zm-3.55 3.55c-.18.18-.45.18-.63 0l-1.42-1.42a.45.45 0 010-.63l1.42-1.42a.45.45 0 01.63 0l1.42 1.42c.18.18.18.45 0 .63l-1.42 1.42z" />
    </svg>
  ),
  Tareas: () => (
    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" strokeWidth={1.5} stroke="currentColor" className="w-5 h-5">
      <path strokeLinecap="round" strokeLinejoin="round" d="M6.75 3v2.25M17.25 3v2.25M3 18.75V7.5a2.25 2.25 0 012.25-2.25h13.5A2.25 2.25 0 0121 7.5v11.25m-18 0A2.25 2.25 0 005.25 21h13.5A2.25 2.25 0 0021 18.75m-18 0v-7.5A2.25 2.25 0 015.25 9h13.5A2.25 2.25 0 0121 11.25v7.5m-9-6h.008v.008H12v-.008zM12 15h.008v.008H12V15zm0 2.25h.008v.008H12v-.008zM9.75 15h.008v.008H9.75V15zm0 2.25h.008v.008H9.75v-.008zM7.5 15h.008v.008H7.5V15zm0 2.25h.008v.008H7.5v-.008zm6.75-4.5h.008v.008h-.008v-.008zm0 2.25h.008v.008h-.008V15zm0 2.25h.008v.008h-.008v-.008zm2.25-4.5h.008v.008H16.5v-.008zm0 2.25h.008v.008H16.5V15z" />
    </svg>
  ),
  Historial: () => (
    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" strokeWidth={1.5} stroke="currentColor" className="w-5 h-5">
      <path strokeLinecap="round" strokeLinejoin="round" d="M12 6v6h4.5m4.5 0a9 9 0 11-18 0 9 9 0 0118 0z" />
    </svg>
  ),
  Reportes: () => (
    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" strokeWidth={1.5} stroke="currentColor" className="w-5 h-5">
      <path strokeLinecap="round" strokeLinejoin="round" d="M3 13.125C3 12.504 3.504 12 4.125 12h2.25c.621 0 1.125.504 1.125 1.125v5.25c0 .621-.504 1.125-1.125 1.125h-2.25A1.125 1.125 0 013 18.375v-5.25zM9.75 8.625c0-.621.504-1.125 1.125-1.125h2.25c.621 0 1.125.504 1.125 1.125v9.75c0 .621-.504 1.125-1.125 1.125h-2.25a1.125 1.125 0 01-1.125-1.125v-9.75zM16.5 4.125c0-.621.504-1.125 1.125-1.125h2.25C20.496 3 21 3.504 21 4.125v14.25c0 .621-.504 1.125-1.125 1.125h-2.25a1.125 1.125 0 01-1.125-1.125V4.125z" />
    </svg>
  ),
  Loto: () => (
    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" strokeWidth={1.5} stroke="currentColor" className="w-5 h-5">
      <path strokeLinecap="round" strokeLinejoin="round" d="M16.5 10.5V6.75a4.5 4.5 0 10-9 0v3.75m-.75 11.25h10.5a2.25 2.25 0 002.25-2.25v-6.75a2.25 2.25 0 00-2.25-2.25H6.75a2.25 2.25 0 00-2.25 2.25v6.75a2.25 2.25 0 002.25 2.25z" />
    </svg>
  ),
  Troubleshooter: () => (
    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" strokeWidth={1.5} stroke="currentColor" className="w-5 h-5">
      <path strokeLinecap="round" strokeLinejoin="round" d="M9.813 15.904L9 21m0 0l-.813-5.096H5.143c-.765 0-1.358-.654-1.23-1.41a2.25 2.25 0 012.23-1.875h2.126M9 21h4.5m0 0l.813-5.096H18.85c.766 0 1.359-.654 1.23-1.41a2.25 2.25 0 00-2.23-1.875h-2.127M12 3c-1.207 0-2.348.332-3.323.913M12 3c1.207 0 2.348.332 3.323.913M12 3v1.5M12 7.5a1.5 1.5 0 110-3 1.5 1.5 0 010 3zM12 11.25a3.75 3.75 0 100-7.5 3.75 3.75 0 000 7.5z" />
    </svg>
  ),
  Asistente: () => (
    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" strokeWidth={1.5} stroke="currentColor" className="w-5 h-5">
      <path strokeLinecap="round" strokeLinejoin="round" d="M19.114 5.636a9 9 0 010 12.728M16.463 8.288a5.25 5.25 0 010 7.424M6.75 8.25l4.72-4.72a.75.75 0 011.28.53v15.88a.75.75 0 01-1.28.53l-4.72-4.72H4.51c-.88 0-1.704-.507-1.938-1.354A9.01 9.01 0 012.25 12c0-.83.112-1.633.322-2.396C2.806 8.756 3.63 8.25 4.51 8.25H6.75z" />
    </svg>
  ),
  Electrico: () => (
    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" strokeWidth={1.5} stroke="currentColor" className="w-5 h-5 text-blue-500">
      <path strokeLinecap="round" strokeLinejoin="round" d="M3.75 13.5l10.5-11.25L12 10.5h8.25L9.75 21.75 12 13.5H3.75z" />
    </svg>
  ),
  Mecanico: () => (
    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" strokeWidth={1.5} stroke="currentColor" className="w-5 h-5 text-orange-500">
      <path strokeLinecap="round" strokeLinejoin="round" d="M4.5 12a7.5 7.5 0 0015 0m-15 0a7.5 7.5 0 1115 0m-15 0H3m16.5 0H21m-1.5 0H12m-8.457 3.077l1.41-.513m11.095-4.028l1.41-.513M5.106 17.785l1.15-.827m9.986-7.17l1.15-.827M8.14 21.27l.707-1.03m6.304-9.19l.707-1.03M12 3v1.5m0 13.5V21m-3.077-16.543l.513 1.41m8.028 11.095l.513 1.41M5.106 6.215l1.15.827m9.986 7.17l1.15.827M8.14 2.73l.707 1.03m6.304 9.19l.707 1.03" />
    </svg>
  ),
  Plus: () => (
    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" strokeWidth={2} stroke="currentColor" className="w-4 h-4">
      <path strokeLinecap="round" strokeLinejoin="round" d="M12 4.5v15m7.5-7.5h-15" />
    </svg>
  ),
  Check: () => (
    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" strokeWidth={2} stroke="currentColor" className="w-4 h-4">
      <path strokeLinecap="round" strokeLinejoin="round" d="M4.5 12.75l6 6 9-13.5" />
    </svg>
  ),
  Warning: () => (
    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" strokeWidth={1.5} stroke="currentColor" className="w-5 h-5 text-red-500">
      <path strokeLinecap="round" strokeLinejoin="round" d="M12 9v3.75m-9.303 3.376c-.866 1.5.217 3.374 1.948 3.374h14.71c1.73 0 2.813-1.874 1.948-3.374L13.949 3.378c-.866-1.5-3.032-1.5-3.898 0L2.697 16.126zM12 15.75h.007v.008H12v-.008z" />
    </svg>
  ),
  Download: () => (
    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" strokeWidth={1.5} stroke="currentColor" className="w-4 h-4">
      <path strokeLinecap="round" strokeLinejoin="round" d="M3 16.5v2.25A2.25 2.25 0 005.25 21h13.5A2.25 2.25 0 0021 18.75V16.5M16.5 12L12 16.5m0 0L7.5 12m4.5 4.5V3" />
    </svg>
  ),
  Reloj: () => (
    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" strokeWidth={1.5} stroke="currentColor" className="w-5 h-5 text-sky-400">
      <path strokeLinecap="round" strokeLinejoin="round" d="M12 6v6h4.5m4.5 0a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" />
    </svg>
  )
};

// --- DATOS INICIALES MOCK ---
const initialEquipos = [
  { id: 'EQ-001', nombre: 'Transformador de Potencia TR-01', tipo: 'Eléctrico', criticidad: 'Alta', ubicacion: 'Subestación Principal', marca: 'Siemens', modelo: 'S9-2000', proximoMantenimiento: '2026-06-15', estado: 'Operativo', anioInstalacion: 2018, confiabilidad: 96 },
  { id: 'EQ-002', nombre: 'Motor Extractor Centrífugo MX-04', tipo: 'Mecánico', criticidad: 'Media', ubicacion: 'Nave de Producción B', marca: 'WEG', modelo: 'W22', proximoMantenimiento: '2026-05-28', estado: 'Mantenimiento Pendiente', anioInstalacion: 2021, confiabilidad: 82 },
  { id: 'EQ-003', nombre: 'Tablero General de Distribución TGD-A', tipo: 'Eléctrico', criticidad: 'Alta', ubicacion: 'Cuarto Eléctrico 1', marca: 'Schneider Electric', modelo: 'PrismaSeT', proximoMantenimiento: '2026-07-10', estado: 'Operativo', anioInstalacion: 2019, confiabilidad: 98 },
  { id: 'EQ-004', nombre: 'Compresor de Aire Tornillo C-02', tipo: 'Mecánico', criticidad: 'Alta', ubicacion: 'Cuarto de Compresores', marca: 'Atlas Copco', modelo: 'GA37', proximoMantenimiento: '2026-05-18', estado: 'Atrasado', anioInstalacion: 2015, confiabilidad: 64 },
  { id: 'EQ-005', nombre: 'Bomba Centrífuga de Agua B-10', tipo: 'Mecánico', criticidad: 'Media', ubicacion: 'Área de Servicios', marca: 'KSB', modelo: 'MegaChem', proximoMantenimiento: '2026-06-05', estado: 'Operativo', anioInstalacion: 2020, confiabilidad: 89 }
];

const initialTareas = [
  { id: 'T-001', equipoId: 'EQ-001', descripcion: 'Termografía y análisis de aceite dieléctrico', frecuencia: 'Semestral', fechaVencimiento: '2026-06-15', prioridad: 'Alta', estado: 'Pendiente', horasHombreEst: 6 },
  { id: 'T-002', equipoId: 'EQ-002', descripcion: 'Lubricación de rodamientos y alineación de ejes', frecuencia: 'Mensual', fechaVencimiento: '2026-05-28', prioridad: 'Media', estado: 'Pendiente', horasHombreEst: 4 },
  { id: 'T-003', equipoId: 'EQ-004', descripcion: 'Cambio de filtros de aire, aceite y separador', frecuencia: 'Trimestral', fechaVencimiento: '2026-05-18', prioridad: 'Alta', estado: 'Atrasado', horasHombreEst: 8 },
  { id: 'T-004', equipoId: 'EQ-003', descripcion: 'Limpieza con solvente dieléctrico y reapriete', frecuencia: 'Anual', fechaVencimiento: '2026-07-10', prioridad: 'Alta', estado: 'Pendiente', horasHombreEst: 5 },
  { id: 'T-005', equipoId: 'EQ-005', descripcion: 'Inspección de sello mecánico y acoplamiento flexible', frecuencia: 'Trimestral', fechaVencimiento: '2026-06-05', prioridad: 'Baja', estado: 'Pendiente', horasHombreEst: 3 }
];

const initialHistorial = [
  { id: 'H-001', equipoId: 'EQ-002', fechaIntervencion: '2026-04-28 09:15', tecnico: 'Carlos Pérez', costo: 150.00, descripcion: 'Cambio preventivo de correa de transmisión y ajuste de tensión.', repuestos: 'Correa en V Optibelt A-42', horasHombreReal: 3.5 },
  { id: 'H-002', equipoId: 'EQ-004', fechaIntervencion: '2026-02-18 14:30', tecnico: 'María Rodríguez', costo: 420.00, descripcion: 'Overhaul menor, cambio de aceite sintético y filtros completos.', repuestos: 'Filtros Atlas Copco Kit 2901', horasHombreReal: 7.0 },
  { id: 'H-003', equipoId: 'EQ-003', fechaIntervencion: '2025-07-10 11:00', tecnico: 'Juan Gómez', costo: 85.00, descripcion: 'Reapriete de borneras y termografía general. Todo en norma.', repuestos: 'N/A', horasHombreReal: 2.0 },
  { id: 'H-004', equipoId: 'EQ-001', fechaIntervencion: '2025-12-15 08:00', tecnico: 'Carlos Pérez', costo: 540.00, descripcion: 'Análisis físico-químico del aceite. Purificación parcial.', repuestos: 'Filtros de celulosa y empaquetaduras', horasHombreReal: 5.5 },
  { id: 'H-005', equipoId: 'EQ-005', fechaIntervencion: '2026-03-05 10:45', tecnico: 'María Rodríguez', costo: 110.00, descripcion: 'Engrase de cojinetes y monitoreo de temperatura.', repuestos: 'Grasa SKF LGHP 2', horasHombreReal: 1.5 }
];

// --- ÁRBOL DE DECISIONES DE DIAGNÓSTICO (TROUBLESHOOTER LOCAL) ---
const diagnosticTree = {
  inicio: {
    pregunta: "¿Qué tipo de activo presenta el síntoma de falla?",
    opciones: [
      { texto: "Motor Eléctrico", destino: "motor" },
      { texto: "Bomba Centrífuga", destino: "bomba" },
      { texto: "Tablero Eléctrico", destino: "tablero" }
    ]
  },
  motor: {
    pregunta: "¿Cuál es el síntoma principal del motor?",
    opciones: [
      { texto: "Calentamiento excesivo de carcasa", destino: "motor_calor" },
      { texto: "Ruido anormal / vibración fuerte", destino: "motor_ruido" }
    ]
  },
  motor_calor: {
    resultado: "Diagnóstico probable: Sobrecarga eléctrica prolongada o bloqueo del ventilador de refrigeración.\n\nRecomendaciones:\n1. Mida corriente en las 3 fases (detectar desbalance).\n2. Verifique que la rejilla del ventilador trasero esté libre de polvo y obstrucciones.\n3. Realice prueba de aislamiento (Megado) de devanados.",
    esFin: true
  },
  motor_ruido: {
    resultado: "Diagnóstico probable: Falla en rodamientos (pista dañada) o desalineación axial de acoplamiento.\n\nRecomendaciones:\n1. Tome espectro de vibraciones. Foco en frecuencias de rodamientos (BPFI/BPFO).\n2. Realice lubricación inmediata con grasa apropiada.\n3. Compruebe la alineación láser con el equipo acoplado.",
    esFin: true
  },
  bomba: {
    pregunta: "¿Qué síntoma experimenta la bomba centrífuga?",
    opciones: [
      { texto: "Pérdida de presión / flujo bajo", destino: "bomba_flujo" },
      { texto: "Ruido como 'bombeo de piedras'", destino: "bomba_cavitacion" }
    ]
  },
  bomba_flujo: {
    resultado: "Diagnóstico probable: Desgaste excesivo del impulsor o entrada de aire en tubería de succión.\n\nRecomendaciones:\n1. Revise el sello mecánico o empaquetadura por posibles fugas.\n2. Limpie la rejilla de succión / válvula de pie.\n3. Mida las tolerancias entre el impulsor y la voluta.",
    esFin: true
  },
  bomba_cavitacion: {
    resultado: "Diagnóstico probable: Cavitación debido a NPSH disponible inferior al requerido.\n\nRecomendaciones:\n1. Verifique si hay válvulas parcialmente cerradas en la línea de succión.\n2. Limpie el filtro de entrada de agua.\n3. Reduzca la temperatura del fluido o aumente el nivel del tanque de succión.",
    esFin: true
  },
  tablero: {
    pregunta: "¿Qué fenómeno se detecta en el tablero general?",
    opciones: [
      { texto: "Disparo continuo de interruptores", destino: "tablero_disparo" },
      { texto: "Olor a quemado / Puntos calientes", destino: "tablero_termografia" }
    ]
  },
  tablero_disparo: {
    resultado: "Diagnóstico probable: Sobrecarga de circuito o cortocircuito franco a tierra.\n\nRecomendaciones:\n1. Mida el consumo de corriente por ramal con pinza amperimétrica.\n2. Verifique la calibración del relé térmico o interruptor magnetotérmico.\n3. Revise aislamiento de cables conductores.",
    esFin: true
  },
  tablero_termografia: {
    resultado: "Diagnóstico probable: Resistencia de contacto alta (falso contacto) por borneras flojas.\n\nRecomendaciones:\n1. Realice termografía infrarroja para identificar el borne con temperatura crítica.\n2. Desenergice el tablero (aplique protocolo LOTO) y reapriete todas las conexiones con torquímetro.\n3. Limpie los contactos oxidados con solvente dieléctrico.",
    esFin: true
  }
};

export default function App() {
  const [activeTab, setActiveTab] = useState('dashboard');
  const [equipos, setEquipos] = useState(initialEquipos);
  const [tareas, setTareas] = useState(initialTareas);
  const [historial, setHistorial] = useState(initialHistorial);

  // Filtros de Equipos y Reportes
  const [filterTipo, setFilterTipo] = useState('Todos');
  const [filterCriticidad, setFilterCriticidad] = useState('Todos');
  const [searchQuery, setSearchQuery] = useState('');

  // Modales
  const [showAddEquipo, setShowAddEquipo] = useState(false);
  const [showAddTarea, setShowAddTarea] = useState(false);
  const [showCompleteTask, setShowCompleteTask] = useState(false);
  const [selectedTaskId, setSelectedTaskId] = useState(null);

  // Estados de Formularios
  const [newEquipo, setNewEquipo] = useState({
    nombre: '', tipo: 'Eléctrico', criticidad: 'Media', ubicacion: '', marca: '', modelo: '', proximoMantenimiento: '', estado: 'Operativo', anioInstalacion: 2020, confiabilidad: 90
  });
  const [newTarea, setNewTarea] = useState({
    equipoId: '', descripcion: '', frecuencia: 'Mensual', fechaVencimiento: '', prioridad: 'Media', horasHombreEst: 4
  });
  const [completionData, setCompletionData] = useState({
    tecnico: '', costo: '', descripcion: '', repuestos: '', horasHombreReal: '', fechaExacta: new Date().toISOString().slice(0, 16)
  });

  // Estado del Asistente IA
  const [aiPrompt, setAiPrompt] = useState('');
  const [aiResponse, setAiResponse] = useState('');
  const [aiLoading, setAiLoading] = useState(false);
  const [selectedEqForAi, setSelectedEqForAi] = useState('');

  // Troubleshooter (Árbol de diagnóstico local)
  const [troubleState, setTroubleState] = useState('inicio');

  // Generador de Tarjeta LOTO
  const [lotoCard, setLotoCard] = useState({
    equipoId: 'EQ-001',
    bloqueadoPor: 'Ernesto Gómez',
    fechaBloqueo: new Date().toISOString().split('T')[0],
    puntosAislamiento: ['Interruptor Termomagnético Principal Q01'],
    tipoEnergia: 'Eléctrica',
    telefonoContacto: '+58 412-5551234'
  });
  const [lotoGenerado, setLotoGenerado] = useState(true);

  // Sincronizar estados de equipos y recalcular confiabilidad basada en fallas/atrasos
  useEffect(() => {
    const hoy = new Date();
    const updatedEquipos = equipos.map(eq => {
      const eqTareas = tareas.filter(t => t.equipoId === eq.id);
      let nuevoEstado = 'Operativo';
      
      if (eqTareas.some(t => t.estado === 'Atrasado' || (new Date(t.fechaVencimiento) < hoy && t.estado !== 'Completado'))) {
        nuevoEstado = 'Atrasado';
      } else if (eqTareas.some(t => t.estado === 'Pendiente')) {
        nuevoEstado = 'Mantenimiento Pendiente';
      }

      // El nivel de confiabilidad disminuye si hay tareas atrasadas o historial muy grande
      const fallas = historial.filter(h => h.equipoId === eq.id).length;
      let nuevoConfiabilidad = 100 - (fallas * 4);
      if (nuevoEstado === 'Atrasado') nuevoConfiabilidad -= 15;
      if (nuevoEstado === 'Mantenimiento Pendiente') nuevoConfiabilidad -= 5;
      nuevoConfiabilidad = Math.max(Math.min(nuevoConfiabilidad, 100), 20);

      return { ...eq, estado: nuevoEstado, confiabilidad: nuevoConfiabilidad };
    });

    if (JSON.stringify(updatedEquipos) !== JSON.stringify(equipos)) {
      setEquipos(updatedEquipos);
    }
  }, [tareas, historial]);

  // Manejador del Asistente IA de Gemini
  const handleAskAI = async (customPrompt = '') => {
    const promptToSend = customPrompt || aiPrompt;
    if (!promptToSend.trim()) return;

    setAiLoading(true);
    setAiResponse('');

    const apiKey = ""; 
    const systemPrompt = "Eres un Ingeniero Senior de Confiabilidad y Mantenimiento Industrial. Proporcionas respuestas estructuradas, precisas y accionables en español sobre diagnóstico de activos mecánicos y eléctricos, análisis predictivo, análisis de modos y efectos de fallas (AMEF) y optimización de costes.";

    const payload = {
      contents: [{ parts: [{ text: promptToSend }] }],
      systemInstruction: { parts: [{ text: systemPrompt }] }
    };

    let retries = 5;
    let delay = 1000;

    while (retries > 0) {
      try {
        const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`, {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(payload)
        });

        if (!response.ok) throw new Error('Error en API');

        const result = await response.json();
        const text = result.candidates?.[0]?.content?.parts?.[0]?.text || "No se obtuvo respuesta de la IA.";
        setAiResponse(text);
        break;
      } catch (error) {
        retries--;
        if (retries === 0) {
          setAiResponse("Lo sentimos, no pudimos conectar con el Asistente de IA de PowerMech en este momento. Por favor, intenta nuevamente.");
        } else {
          await new Promise(resolve => setTimeout(resolve, delay));
          delay *= 2;
        }
      }
    }
    setAiLoading(false);
  };

  const triggerAiReportAudit = () => {
    setActiveTab('asistente');
    const systemDataSummary = `Tengo ${equipos.length} activos registrados. Las intervenciones completadas suman un costo acumulado de $${historial.reduce((acc, c) => acc + c.costo, 0)} y un total de ${historial.reduce((acc, c) => a
