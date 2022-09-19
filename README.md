# web1
ExamenWeb1
let jugadores = [
    {
        nombre: "Jugador 1",
        marcador: "X"
    },
    {
        nombre: "Jugador 2",
        marcador: "O"
    }
]
let actualJugador = jugadores[0]
let turnoP2 = false
let gameover = false

const marcos = document.getElementsByClassName("marcos")

const estado = document.getElementById("estado")

const verificarTurno = () => {
    if(turnoP2) {
        actualJugador = jugadores[1]
    } else {
        actualJugador = jugadores[0]
    }
    estado.textContent = `Turno del jugador ${actualJugador.nombre}`
}

const verificarGanador = () => {
    let arr = []
    for (const marco of marcos) {
        arr.push(marco.children[0].textContent)
    }
    // Sí verifica que son iguales
    console.log(arr[0], arr[4], arr[8])
    // Lógica
    if (arr[0] === arr[1] === arr[2]) {
        estado.textContent = `Ganador: ${actualJugador.nombre}`
        gameover = true
    } else if (arr[0] === arr[4] === arr[8]) {
        estado.textContent = `Ganador: ${actualJugador.nombre}`
        gameover = true
    } else if (arr[0] === arr[3] === arr[6]) {
        estado.textContent = `Ganador: ${actualJugador.nombre}`
        gameover = true
    } else if (arr[1] === arr[4] === arr[7]) {
        estado.textContent = `Ganador: ${actualJugador.nombre}`
        gameover = true
    } else if (arr[2] === arr[5] === arr[8]) {
        estado.textContent = `Ganador: ${actualJugador.nombre}`
        gameover = true
    } else if (arr[2] === arr[4] === arr[6]) {
        estado.textContent = `Ganador: ${actualJugador.nombre}`
        gameover = true
    } else {
        verificarTurno()
    }
    // console.log(gameover)
}

const marcar = (e) => {
    if(gameover) {
        estado.textContent = "El juego ha terminado"
    } else {
        if(e.target.disabled) {
            estado.textContent = "Caseta marcada. Por favor, elija otra"
        } else {
            e.target.innerText = actualJugador.marcador
            e.target.disabled = true
            turnoP2 = !turnoP2
            verificarGanador()
            // verificarTurno()
        }
    }
    
}

for (const marco of marcos) {
    const button = marco.querySelector("button")
    button.addEventListener("click", marcar)
}
