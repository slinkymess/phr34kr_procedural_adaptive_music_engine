# phr34kr_procedural_adaptive_music_engine
phr34kr // Procedural Adaptive Music Engine
phr34kr (v1.0) is a lightweight, zero-dependency procedural soundtrack engine designed for cyberpunk hacker fighting games and high-intensity action titles.
Instead of playing static audio tracks, phr34kr procedurally generates 90s-inspired atmospheric soundtracks from 32-Bit Hex Seeds (0x...) and seamlessly evolves the music in real time based on a gameplay Combat Intensity (0% to 100%) signal.
Key Features
Infinite Hex Track Seeds: Every game session generates a unique track seed (e.g. NEURAL_DRIFT [0x9F42]). No two tracks sound alike.
Sample-Accurate Lookahead Scheduler: Grid-locked 16th-note lookahead scheduler prevents audio jumbling or timing breaks when combat intensity rapidly spikes.
Rich 90s Cyberpunk Synth Palette:
Lush Ambient Pad: Multi-oscillator sub sweeps for stealth phases.
Reese Bass: Dual detuned sawtooth bass with dynamic filter sweeps.
303 Acid Lead: Resonant squealing filter sweeps for mid-combat aggression.
FM Cyber Pluck: Metallic frequency-modulated chimes.
Liquid 90s Drums: Non-chaotic, driving drum and bass grooves.
Micro-Glitch Engine: 32nd-note stutters and deep reverb washes during climax phases.
Smooth Volume & Tempo Interpolation: Starts at a confident baseline (~70% volume) and ramps smoothly from 100 BPM to 142 BPM without harsh jumps.
Directory Structure
phr34kr/
├── index.html        # Web Application & Interactive Engine Simulator
├── phr34kr.gd        # Native Godot 4.x GDScript Audio Engine Node
└── README.md         # Documentation & Integration SDK


Integration Guide
1. Web Engine (JavaScript / HTML5)
For web games built in Canvas, Three.js, or Phaser:
// Initialize phr34kr audio engine
const audioEngine = new Phr34krAudioEngine();

// Call when starting a new match
audioEngine.startNewGame(); // Generates a new Hex seed & track title

// Connect to player attack / damage event listeners
function onPlayerHit() {
  audioEngine.setIntensity(currentFightIntensity); // 0.0 to 1.0
}


2. Godot 4 Engine Integration (GDScript)
Attach phr34kr.gd to a Node in your Godot project scene:
extends Node2D

@onready var phr34kr = $Phr34krEngine

func _ready():
    # Start new game track
    phr34kr.start_new_game()
    phr34kr.start_audio()

func _on_player_combo_hit(combo_count: int):
    # Dynamically scale combat intensity
    var intensity_val = clamp(combo_count * 0.15, 0.0, 1.0)
    phr34kr.set_intensity(intensity_val)


License
GNU General Public License v3.0
