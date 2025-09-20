<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bộ Trò Chơi Luyện Vần</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Pacifico&family=Inter:wght@400;700&display=swap');
        
        body {
            font-family: 'Inter', 'Arial Unicode MS', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 10px;
            overflow: hidden;
            background-color: #f0f8ff; /* Default background */
            transition: background-color 0.5s ease-in-out;
        }

        .game-container {
            max-width: 800px;
            width: 98%;
            padding: 1rem;
            background-color: #fff;
            border-radius: 2rem;
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.1);
            border: 5px solid #e0e0e0;
            text-align: center;
            position: relative;
            z-index: 10;
        }
        
        .title {
            font-family: 'Pacifico', cursive;
            font-size: 2.5rem;
            color: #4a90e2;
            margin-bottom: 1rem;
            text-shadow: 2px 2px 0 #fff;
        }
        
        .nav-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 0.5rem;
            margin-bottom: 1.5rem;
            max-height: 150px;
            overflow-y: auto;
            padding-right: 10px;
        }

        .nav-btn {
            background-color: #a0a0a0;
            color: white;
            padding: 0.4rem 0.6rem;
            font-size: 0.9rem;
            font-weight: bold;
            border-radius: 9999px;
            cursor: pointer;
            transition: all 0.2s ease-in-out;
        }

        .nav-btn:hover, .nav-btn.active {
            background-color: #4a90e2;
            transform: scale(1.1);
        }

        .sentence-display {
            min-height: 100px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.8rem;
            font-weight: bold;
            color: #3d3d3d;
            padding: 0.8rem;
            background-color: #f7f7f7;
            border-radius: 1.5rem;
            margin-bottom: 1.2rem;
            box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.06);
            border: 2px dashed #a0a0a0;
            line-height: 1.5;
            transition: all 0.3s ease-in-out;
            flex-wrap: wrap;
        }

        .sentence-display span {
            display: inline-block;
        }

        .icon {
            margin: 0 0.4rem;
            font-size: 2rem;
            vertical-align: middle;
        }

        .controls {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: 1.5rem;
        }

        .btn {
            background-color: #4a90e2;
            color: white;
            padding: 0.4rem 0.6rem;
            font-size: 1rem;
            font-weight: bold;
            border-radius: 9999px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1), 0 1px 3px rgba(0, 0, 0, 0.08);
            transition: all 0.2s ease-in-out;
            cursor: pointer;
            border: 3px solid white;
            display: flex;
            align-items: center;
            gap: 0.25rem;
        }

        .btn:hover:not(:disabled) {
            transform: translateY(-3px);
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15), 0 2px 4px rgba(0, 0, 0, 0.1);
            background-color: #357bd9;
        }
        
        .btn:active:not(:disabled) {
            transform: translateY(0);
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1), 0 1px 2px rgba(0, 0, 0, 0.08);
        }

        .btn:disabled {
            background-color: #ccc;
            cursor: not-allowed;
            box-shadow: none;
        }
        
        .btn-text {
            display: none;
        }
        .btn-icon {
            display: block;
        }

        .read-btn {
            background-color: #ff69b4;
            color: #fff;
            font-size: 1rem;
            padding: 0.4rem 0.8rem;
            border-radius: 9999px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            border: 3px solid white;
            transition: all 0.2s ease-in-out;
            cursor: pointer;
            margin-top: 1rem;
            font-weight: bold;
        }
        
        .read-btn:hover:not(:disabled) {
            transform: scale(1.05);
            background-color: #c71585;
        }

        .read-btn:active:not(:disabled) {
            transform: scale(1);
        }

        .read-btn:disabled {
            background-color: #ccc;
            color: #999;
            cursor: not-allowed;
        }

        .record-controls {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 1rem;
            margin-top: 1rem;
        }

        .record-btn, .playback-btn {
            background-color: #17c1d7;
            color: #fff;
            padding: 0.6rem 1.2rem;
            font-size: 1rem;
            border-radius: 9999px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            border: 3px solid white;
            transition: all 0.2s ease-in-out;
            cursor: pointer;
        }
        
        .record-btn:hover:not(:disabled), .playback-btn:hover:not(:disabled) {
            background-color: #129fae;
        }
        .record-btn:active:not(:disabled), .playback-btn:active:not(:disabled) {
            transform: translateY(0);
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1), 0 1px 2px rgba(0, 0, 0, 0.08);
        }

        .record-btn.recording {
            background-color: #c71585;
            animation: pulse 1s infinite;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }

        .record-btn:disabled, .playback-btn:disabled {
            background-color: #ccc;
            cursor: not-allowed;
            box-shadow: none;
        }

        .counter {
            font-size: 1.2rem;
            font-weight: bold;
            color: #4a90e2;
            text-shadow: 1px 1px 0 #fff;
        }

        .loading {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 20;
            background: rgba(255, 255, 255, 0.8);
            padding: 20px;
            border-radius: 10px;
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }

        .loading-spinner {
            border: 4px solid #f3f3f3;
            border-top: 4px solid #4a90e2;
            border-radius: 50%;
            width: 30px;
            height: 30px;
            animation: spin 1s linear infinite;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .timer-container {
            font-size: 1rem;
            font-weight: bold;
            color: #4a90e2;
            margin-top: 1rem;
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 0.5rem;
        }

        .timer-btn {
            padding: 0.2rem 0.5rem;
            font-size: 0.9rem;
            background-color: #4a90e2;
            color: white;
            border-radius: 9999px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            transition: transform 0.2s;
            cursor: pointer;
        }

        .timer-btn:hover {
            transform: scale(1.05);
        }
        
        @media (min-width: 641px) {
            .btn-text {
                display: block;
            }
            .btn-icon {
                display: none;
            }
            .btn {
                padding: 0.5rem 0.8rem;
            }
        }

        /* --- Theme-specific styles --- */
        .theme-ai { background-color: #fce8a9; }
        .theme-ai .game-container { border-color: #ffcc00; }
        .theme-ai .title, .theme-ai .counter, .theme-ai .timer-container { color: #ffcc00; }
        .theme-ai .btn, .theme-ai .timer-btn { background-color: #ffd700; border-color: #fff; }
        .theme-ai .btn:hover:not(:disabled), .theme-ai .timer-btn:hover { background-color: #ffc200; }
        .theme-ai .sentence-display { background-color: #fffacd; border-color: #ffcc00; }
        .theme-ai .loading-spinner { border-top-color: #ffcc00; }
        .theme-ai .nav-btn.active { background-color: #ffcc00; }

        .theme-oi { background-color: #e6e6fa; } 
        .theme-oi .game-container { border-color: #9370db; }
        .theme-oi .title, .theme-oi .counter, .theme-oi .timer-container { color: #9370db; }
        .theme-oi .btn, .theme-oi .timer-btn { background-color: #9370db; border-color: #fff; }
        .theme-oi .btn:hover:not(:disabled), .theme-oi .timer-btn:hover { background-color: #8a2be2; }
        .theme-oi .sentence-display { background-color: #f8f8ff; border-color: #9370db; }
        .theme-oi .loading-spinner { border-top-color: #9370db; }
        .theme-oi .nav-btn.active { background-color: #9370db; }

        .theme-on { background-color: #f0f8ff; } 
        .theme-on .game-container { border-color: #4a90e2; }
        .theme-on .title, .theme-on .counter, .theme-on .timer-container { color: #4a90e2; }
        .theme-on .btn, .theme-on .timer-btn { background-color: #4a90e2; border-color: #fff; }
        .theme-on .btn:hover:not(:disabled), .theme-on .timer-btn:hover { background-color: #357bd9; }
        .theme-on .sentence-display { background-color: #c8e6c9; border-color: #4a90e2; }
        .theme-on .loading-spinner { border-top-color: #4a90e2; }
        .theme-on .nav-btn.active { background-color: #4a90e2; }

        .theme-an { background-color: #ffcc99; }
        .theme-an .game-container { border-color: #ff9933; }
        .theme-an .title, .theme-an .counter, .theme-an .timer-container { color: #ff9933; }
        .theme-an .btn, .theme-an .timer-btn { background-color: #ff9933; border-color: #fff; }
        .theme-an .btn:hover:not(:disabled), .theme-an .timer-btn:hover { background-color: #ff8c00; }
        .theme-an .sentence-display { background-color: #fff0e0; border-color: #ff9933; }
        .theme-an .loading-spinner { border-top-color: #ff9933; }
        .theme-an .nav-btn.active { background-color: #ff9933; }

        .theme-ua { background-color: #f7e9f7; } 
        .theme-ua .game-container { border-color: #d889d8; }
        .theme-ua .title, .theme-ua .counter, .theme-ua .timer-container { color: #d889d8; }
        .theme-ua .btn, .theme-ua .timer-btn { background-color: #d889d8; border-color: #fff; }
        .theme-ua .btn:hover:not(:disabled), .theme-ua .timer-btn:hover { background-color: #c960c9; }
        .theme-ua .sentence-display { background-color: #ffe4e1; border-color: #d889d8; }
        .theme-ua .loading-spinner { border-top-color: #d889d8; }
        .theme-ua .nav-btn.active { background-color: #d889d8; }

        .theme-uu { background-color: #e0f2f1; }
        .theme-uu .game-container { border-color: #2e8b57; }
        .theme-uu .title, .theme-uu .counter, .theme-uu .timer-container { color: #2e8b57; }
        .theme-uu .btn, .theme-uu .timer-btn { background-color: #2e8b57; border-color: #fff; }
        .theme-uu .btn:hover:not(:disabled), .theme-uu .timer-btn:hover { background-color: #1f6b43; }
        .theme-uu .sentence-display { background-color: #d4edda; border-color: #2e8b57; }
        .theme-uu .loading-spinner { border-top-color: #2e8b57; }
        .theme-uu .nav-btn.active { background-color: #2e8b57; }

        .theme-a-mu { background-color: #fff8e1; }
        .theme-a-mu .game-container { border-color: #f99061; }
        .theme-a-mu .title, .theme-a-mu .counter, .theme-a-mu .timer-container { color: #f99061; }
        .theme-a-mu .btn, .theme-a-mu .timer-btn { background-color: #f99061; border-color: #fff; }
        .theme-a-mu .btn:hover:not(:disabled), .theme-a-mu .timer-btn:hover { background-color: #f47b4d; }
        .theme-a-mu .sentence-display { background-color: #fffacd; border-color: #f99061; }
        .theme-a-mu .loading-spinner { border-top-color: #f99061; }
        .theme-a-mu .nav-btn.active { background-color: #f99061; }

        .theme-a-mo { background-color: #b0e0e6; }
        .theme-a-mo .game-container { border-color: #4682b4; }
        .theme-a-mo .title, .theme-a-mo .counter, .theme-a-mo .timer-container { color: #4682b4; }
        .theme-a-mo .btn, .theme-a-mo .timer-btn { background-color: #4682b4; border-color: #fff; }
        .theme-a-mo .btn:hover:not(:disabled), .theme-a-mo .timer-btn:hover { background-color: #2e648e; }
        .theme-a-mo .sentence-display { background-color: #add8e6; border-color: #4682b4; }
        .theme-a-mo .loading-spinner { border-top-color: #4682b4; }
        .theme-a-mo .nav-btn.active { background-color: #4682b4; }
        
        .theme-oi-hat { background-color: #e6e6fa; } 
        .theme-oi-hat .game-container { border-color: #9370db; }
        .theme-oi-hat .title, .theme-oi-hat .counter, .theme-oi-hat .timer-container { color: #9370db; }
        .theme-oi-hat .btn, .theme-oi-hat .timer-btn { background-color: #9370db; border-color: #fff; }
        .theme-oi-hat .btn:hover:not(:disabled), .theme-oi-hat .timer-btn:hover { background-color: #8a2be2; }
        .theme-oi-hat .sentence-display { background-color: #f8f8ff; border-color: #9370db; }
        .theme-oi-hat .loading-spinner { border-top-color: #9370db; }
        .theme-oi-hat .nav-btn.active { background-color: #9370db; }
        
        .theme-oi-mo { background-color: #f0fff0; }
        .theme-oi-mo .game-container { border-color: #228b22; }
        .theme-oi-mo .title, .theme-oi-mo .counter, .theme-oi-mo .timer-container { color: #228b22; }
        .theme-oi-mo .btn, .theme-oi-mo .timer-btn { background-color: #228b22; border-color: #fff; }
        .theme-oi-mo .btn:hover:not(:disabled), .theme-oi-mo .timer-btn:hover { background-color: #176417; }
        .theme-oi-mo .sentence-display { background-color: #c8e6c9; border-color: #228b22; }
        .theme-oi-mo .loading-spinner { border-top-color: #228b22; }
        .theme-oi-mo .nav-btn.active { background-color: #228b22; }
        
        .theme-en { background-color: #ffe4e1; }
        .theme-en .game-container { border-color: #d889d8; }
        .theme-en .title, .theme-en .counter, .theme-en .timer-container { color: #d889d8; }
        .theme-en .btn, .theme-en .timer-btn { background-color: #d889d8; border-color: #fff; }
        .theme-en .btn:hover:not(:disabled), .theme-en .timer-btn:hover { background-color: #c960c9; }
        .theme-en .sentence-display { background-color: #fff0f0; border-color: #d889d8; }
        .theme-en .loading-spinner { border-top-color: #d889d8; }
        .theme-en .nav-btn.active { background-color: #d889d8; }
        
        .theme-en-hat { background-color: #b0e0e6; }
        .theme-en-hat .game-container { border-color: #4682b4; }
        .theme-en-hat .title, .theme-en-hat .counter, .theme-en-hat .timer-container { color: #4682b4; }
        .theme-en-hat .btn, .theme-en-hat .timer-btn { background-color: #4682b4; border-color: #fff; }
        .theme-en-hat .btn:hover:not(:disabled), .theme-en-hat .timer-btn:hover { background-color: #2e648e; }
        .theme-en-hat .sentence-display { background-color: #add8e6; border-color: #4682b4; }
        .theme-en-hat .loading-spinner { border-top-color: #4682b4; }
        .theme-en-hat .nav-btn.active { background-color: #4682b4; }
        
        .theme-ay { background-color: #f6e4a2; }
        .theme-ay .game-container { border-color: #f99061; }
        .theme-ay .title, .theme-ay .counter, .theme-ay .timer-container { color: #f99061; }
        .theme-ay .btn, .theme-ay .timer-btn { background-color: #f99061; border-color: #fff; }
        .theme-ay .btn:hover:not(:disabled), .theme-ay .timer-btn:hover { background-color: #f47b4d; }
        .theme-ay .sentence-display { background-color: #fff8e1; border-color: #f99061; }
        .theme-ay .loading-spinner { border-top-color: #f99061; }
        .theme-ay .nav-btn.active { background-color: #f99061; }
        
        .theme-ay-hat { background-color: #e6e6fa; }
        .theme-ay-hat .game-container { border-color: #9370db; }
        .theme-ay-hat .title, .theme-ay-hat .counter, .theme-ay-hat .timer-container { color: #9370db; }
        .theme-ay-hat .btn, .theme-ay-hat .timer-btn { background-color: #9370db; border-color: #fff; }
        .theme-ay-hat .btn:hover:not(:disabled), .theme-ay-hat .timer-btn:hover { background-color: #8a2be2; }
        .theme-ay-hat .sentence-display { background-color: #f8f8ff; border-color: #9370db; }
        .theme-ay-hat .loading-spinner { border-top-color: #9370db; }
        .theme-ay-hat .nav-btn.active { background-color: #9370db; }

        .theme-om { background-color: #fce8a9; }
        .theme-om .game-container { border-color: #ffcc00; }
        .theme-om .title, .theme-om .counter, .theme-om .timer-container { color: #ffcc00; }
        .theme-om .btn, .theme-om .timer-btn { background-color: #ffd700; border-color: #fff; }
        .theme-om .btn:hover:not(:disabled), .theme-om .timer-btn:hover { background-color: #ffc200; }
        .theme-om .sentence-display { background-color: #fffacd; border-color: #ffcc00; }
        .theme-om .loading-spinner { border-top-color: #ffcc00; }
        .theme-om .nav-btn.active { background-color: #ffcc00; }

        .theme-am { background-color: #ffcc99; }
        .theme-am .game-container { border-color: #ff9933; }
        .theme-am .title, .theme-am .counter, .theme-am .timer-container { color: #ff9933; }
        .theme-am .btn, .theme-am .timer-btn { background-color: #ff9933; border-color: #fff; }
        .theme-am .btn:hover:not(:disabled), .theme-am .timer-btn:hover { background-color: #ff8c00; }
        .theme-am .sentence-display { background-color: #fff0e0; border-color: #ff9933; }
        .theme-am .loading-spinner { border-top-color: #ff9933; }
        .theme-am .nav-btn.active { background-color: #ff9933; }
        
        .theme-au { background-color: #f0f8ff; }
        .theme-au .game-container { border-color: #4a90e2; }
        .theme-au .title, .theme-au .counter, .theme-au .timer-container { color: #4a90e2; }
        .theme-au .btn, .theme-au .timer-btn { background-color: #4a90e2; border-color: #fff; }
        .theme-au .btn:hover:not(:disabled), .theme-au .timer-btn:hover { background-color: #357bd9; }
        .theme-au .sentence-display { background-color: #c8e6c9; border-color: #4a90e2; }
        .theme-au .loading-spinner { border-top-color: #4a90e2; }
        .theme-au .nav-btn.active { background-color: #4a90e2; }
        
        .theme-au-hat { background-color: #f7e9f7; } 
        .theme-au-hat .game-container { border-color: #d889d8; }
        .theme-au-hat .title, .theme-au-hat .counter, .theme-au-hat .timer-container { color: #d889d8; }
        .theme-au-hat .btn, .theme-au-hat .timer-btn { background-color: #d889d8; border-color: #fff; }
        .theme-au-hat .btn:hover:not(:disabled), .theme-au-hat .timer-btn:hover { background-color: #c960c9; }
        .theme-au-hat .sentence-display { background-color: #ffe4e1; border-color: #d889d8; }
        .theme-au-hat .loading-spinner { border-top-color: #d889d8; }
        .theme-au-hat .nav-btn.active { background-color: #d889d8; }

        .theme-uon { background-color: #f0fff0; }
        .theme-uon .game-container { border-color: #228b22; }
        .theme-uon .title, .theme-uon .counter, .theme-uon .timer-container { color: #228b22; }
        .theme-uon .btn, .theme-uon .timer-btn { background-color: #228b22; border-color: #fff; }
        .theme-uon .btn:hover:not(:disabled), .theme-uon .timer-btn:hover { background-color: #176417; }
        .theme-uon .sentence-display { background-color: #c8e6c9; border-color: #228b22; }
        .theme-uon .loading-spinner { border-top-color: #228b22; }
        .theme-uon .nav-btn.active { background-color: #228b22; }
        
        .theme-uon-mo { background-color: #b0e0e6; }
        .theme-uon-mo .game-container { border-color: #4682b4; }
        .theme-uon-mo .title, .theme-uon-mo .counter, .theme-uon-mo .timer-container { color: #4682b4; }
        .theme-uon-mo .btn, .theme-uon-mo .timer-btn { background-color: #4682b4; border-color: #fff; }
        .theme-uon-mo .btn:hover:not(:disabled), .theme-uon-mo .timer-btn:hover { background-color: #2e648e; }
        .theme-uon-mo .sentence-display { background-color: #add8e6; border-color: #4682b4; }
        .theme-uon-mo .loading-spinner { border-top-color: #4682b4; }
        .theme-uon-mo .nav-btn.active { background-color: #4682b4; }
        
        .theme-on-hat { background-color: #fff8e1; }
        .theme-on-hat .game-container { border-color: #f99061; }
        .theme-on-hat .title, .theme-on-hat .counter, .theme-on-hat .timer-container { color: #f99061; }
        .theme-on-hat .btn, .theme-on-hat .timer-btn { background-color: #f99061; border-color: #fff; }
        .theme-on-hat .btn:hover:not(:disabled), .theme-on-hat .timer-btn:hover { background-color: #f47b4d; }
        .theme-on-hat .sentence-display { background-color: #fffacd; border-color: #f99061; }
        .theme-on-hat .loading-spinner { border-top-color: #f99061; }
        .theme-on-hat .nav-btn.active { background-color: #f99061; }
        
        .theme-on-mo { background-color: #fce8e8; }
        .theme-on-mo .game-container { border-color: #e06666; }
        .theme-on-mo .title, .theme-on-mo .counter, .theme-on-mo .timer-container { color: #e06666; }
        .theme-on-mo .btn, .theme-on-mo .timer-btn { background-color: #e06666; border-color: #fff; }
        .theme-on-mo .btn:hover:not(:disabled), .theme-on-mo .timer-btn:hover { background-color: #cc3333; }
        .theme-on-mo .sentence-display { background-color: #fff0f0; border-color: #e06666; }
        .theme-on-mo .loading-spinner { border-top-color: #e06666; }
        .theme-on-mo .nav-btn.active { background-color: #e06666; }
        
        .theme-eo { background-color: #f5f5dc; }
        .theme-eo .game-container { border-color: #ff6347; }
        .theme-eo .title, .theme-eo .counter, .theme-eo .timer-container { color: #ff6347; }
        .theme-eo .btn, .theme-eo .timer-btn { background-color: #ff6347; border-color: #fff; }
        .theme-eo .btn:hover:not(:disabled), .theme-eo .timer-btn:hover { background-color: #e5533d; }
        .theme-eo .sentence-display { background-color: #ffe4e1; border-color: #ff6347; }
        .theme-eo .loading-spinner { border-top-color: #ff6347; }
        .theme-eo .nav-btn.active { background-color: #ff6347; }
        
        .theme-ao { background-color: #ffb6c1; }
        .theme-ao .game-container { border-color: #ff69b4; }
        .theme-ao .title, .theme-ao .counter, .theme-ao .timer-container { color: #ff69b4; }
        .theme-ao .btn, .theme-ao .timer-btn { background-color: #ff69b4; border-color: #fff; }
        .theme-ao .btn:hover:not(:disabled), .theme-ao .timer-btn:hover { background-color: #c71585; }
        .theme-ao .sentence-display { background-color: #ffe4e1; border-color: #ff69b4; }
        .theme-ao .loading-spinner { border-top-color: #ff69b4; }
        .theme-ao .nav-btn.active { background-color: #ff69b4; }

        .theme-ong { background-color: #f8f8f2; }
        .theme-ong .game-container { border-color: #8b4513; }
        .theme-ong .title, .theme-ong .counter, .theme-ong .timer-container { color: #8b4513; }
        .theme-ong .btn, .theme-ong .timer-btn { background-color: #8b4513; border-color: #fff; }
        .theme-ong .btn:hover:not(:disabled), .theme-ong .timer-btn:hover { background-color: #6d330c; }
        .theme-ong .sentence-display { background-color: #f5deb3; border-color: #8b4513; }
        .theme-ong .loading-spinner { border-top-color: #8b4513; }
        .theme-ong .nav-btn.active { background-color: #8b4513; }

        .theme-ong-hat { background-color: #fce8e8; }
        .theme-ong-hat .game-container { border-color: #e06666; }
        .theme-ong-hat .title, .theme-ong-hat .counter, .theme-ong-hat .timer-container { color: #e06666; }
        .theme-ong-hat .btn, .theme-ong-hat .timer-btn { background-color: #e06666; border-color: #fff; }
        .theme-ong-hat .btn:hover:not(:disabled), .theme-ong-hat .timer-btn:hover { background-color: #cc3333; }
        .theme-ong-hat .sentence-display { background-color: #fff0f0; border-color: #e06666; }
        .theme-ong-hat .loading-spinner { border-top-color: #e06666; }
        .theme-ong-hat .nav-btn.active { background-color: #e06666; }
        
        .theme-em { background-color: #fff8e1; }
        .theme-em .game-container { border-color: #f99061; }
        .theme-em .title, .theme-em .counter, .theme-em .timer-container { color: #f99061; }
        .theme-em .btn, .theme-em .timer-btn { background-color: #f99061; border-color: #fff; }
        .theme-em .btn:hover:not(:disabled), .theme-em .timer-btn:hover { background-color: #f47b4d; }
        .theme-em .sentence-display { background-color: #fffacd; border-color: #f99061; }
        .theme-em .loading-spinner { border-top-color: #f99061; }
        .theme-em .nav-btn.active { background-color: #f99061; }

        .theme-em-hat { background-color: #e6e6fa; }
        .theme-em-hat .game-container { border-color: #9370db; }
        .theme-em-hat .title, .theme-em-hat .counter, .theme-em-hat .timer-container { color: #9370db; }
        .theme-em-hat .btn, .theme-em-hat .timer-btn { background-color: #9370db; border-color: #fff; }
        .theme-em-hat .btn:hover:not(:disabled), .theme-em-hat .timer-btn:hover { background-color: #8a2be2; }
        .theme-em-hat .sentence-display { background-color: #f8f8ff; border-color: #9370db; }
        .theme-em-hat .loading-spinner { border-top-color: #9370db; }
        .theme-em-hat .nav-btn.active { background-color: #9370db; }

        .theme-im { background-color: #f0f8ff; }
        .theme-im .game-container { border-color: #4a90e2; }
        .theme-im .title, .theme-im .counter, .theme-im .timer-container { color: #4a90e2; }
        .theme-im .btn, .theme-im .timer-btn { background-color: #4a90e2; border-color: #fff; }
        .theme-im .btn:hover:not(:disabled), .theme-im .timer-btn:hover { background-color: #357bd9; }
        .theme-im .sentence-display { background-color: #c8e6c9; border-color: #4a90e2; }
        .theme-im .loading-spinner { border-top-color: #4a90e2; }
        .theme-im .nav-btn.active { background-color: #4a90e2; }
        
        .theme-um { background-color: #e0f2f1; }
        .theme-um .game-container { border-color: #2e8b57; }
        .theme-um .title, .theme-um .counter, .theme-um .timer-container { color: #2e8b57; }
        .theme-um .btn, .theme-um .timer-btn { background-color: #2e8b57; border-color: #fff; }
        .theme-um .btn:hover:not(:disabled), .theme-um .timer-btn:hover { background-color: #1f6b43; }
        .theme-um .sentence-display { background-color: #d4edda; border-color: #2e8b57; }
        .theme-um .loading-spinner { border-top-color: #2e8b57; }
        .theme-um .nav-btn.active { background-color: #2e8b57; }

        .theme-in { background-color: #fce8e8; }
        .theme-in .game-container { border-color: #e06666; }
        .theme-in .title, .theme-in .counter, .theme-in .timer-container { color: #e06666; }
        .theme-in .btn, .theme-in .timer-btn { background-color: #e06666; border-color: #fff; }
        .theme-in .btn:hover:not(:disabled), .theme-in .timer-btn:hover { background-color: #cc3333; }
        .theme-in .sentence-display { background-color: #fff0f0; border-color: #e06666; }
        .theme-in .loading-spinner { border-top-color: #e06666; }
        .theme-in .nav-btn.active { background-color: #e06666; }

        .theme-un { background-color: #f8f8f2; }
        .theme-un .game-container { border-color: #8b4513; }
        .theme-un .title, .theme-un .counter, .theme-un .timer-container { color: #8b4513; }
        .theme-un .btn, .theme-un .timer-btn { background-color: #8b4513; border-color: #fff; }
        .theme-un .btn:hover:not(:disabled), .theme-un .timer-btn:hover { background-color: #6d330c; }
        .theme-un .sentence-display { background-color: #f5deb3; border-color: #8b4513; }
        .theme-un .loading-spinner { border-top-color: #8b4513; }
        .theme-un .nav-btn.active { background-color: #8b4513; }
        
        .theme-om-hat { background-color: #fff8e1; }
        .theme-om-hat .game-container { border-color: #f99061; }
        .theme-om-hat .title, .theme-om-hat .counter, .theme-om-hat .timer-container { color: #f99061; }
        .theme-om-hat .btn, .theme-om-hat .timer-btn { background-color: #f99061; border-color: #fff; }
        .theme-om-hat .btn:hover:not(:disabled), .theme-om-hat .timer-btn:hover { background-color: #f47b4d; }
        .theme-om-hat .sentence-display { background-color: #fffacd; border-color: #f99061; }
        .theme-om-hat .loading-spinner { border-top-color: #f99061; }
        .theme-om-hat .nav-btn.active { background-color: #f99061; }
        
        .theme-om-mo { background-color: #ffb6c1; }
        .theme-om-mo .game-container { border-color: #ff69b4; }
        .theme-om-mo .title, .theme-om-mo .counter, .theme-om-mo .timer-container { color: #ff69b4; }
        .theme-om-mo .btn, .theme-om-mo .timer-btn { background-color: #ff69b4; border-color: #fff; }
        .theme-om-mo .btn:hover:not(:disabled), .theme-om-mo .timer-btn:hover { background-color: #c71585; }
        .theme-om-mo .sentence-display { background-color: #ffe4e1; border-color: #ff69b4; }
        .theme-om-mo .loading-spinner { border-top-color: #ff69b4; }
        .theme-om-mo .nav-btn.active { background-color: #ff69b4; }
        
        .theme-iu { background-color: #e6e6fa; }
        .theme-iu .game-container { border-color: #9370db; }
        .theme-iu .title, .theme-iu .counter, .theme-iu .timer-container { color: #9370db; }
        .theme-iu .btn, .theme-iu .timer-btn { background-color: #9370db; border-color: #fff; }
        .theme-iu .btn:hover:not(:disabled), .theme-iu .timer-btn:hover { background-color: #8a2be2; }
        .theme-iu .sentence-display { background-color: #f8f8ff; border-color: #9370db; }
        .theme-iu .loading-spinner { border-top-color: #9370db; }
        .theme-iu .nav-btn.active { background-color: #9370db; }
        
        .theme-eu { background-color: #f0f8ff; }
        .theme-eu .game-container { border-color: #4a90e2; }
        .theme-eu .title, .theme-eu .counter, .theme-eu .timer-container { color: #4a90e2; }
        .theme-eu .btn, .theme-eu .timer-btn { background-color: #4a90e2; border-color: #fff; }
        .theme-eu .btn:hover:not(:disabled), .theme-eu .timer-btn:hover { background-color: #357bd9; }
        .theme-eu .sentence-display { background-color: #c8e6c9; border-color: #4a90e2; }
        .theme-eu .loading-spinner { border-top-color: #4a90e2; }
        .theme-eu .nav-btn.active { background-color: #4a90e2; }
        
        .theme-ui { background-color: #f7e9f7; }
        .theme-ui .game-container { border-color: #d889d8; }
        .theme-ui .title, .theme-ui .counter, .theme-ui .timer-container { color: #d889d8; }
        .theme-ui .btn, .theme-ui .timer-btn { background-color: #d889d8; border-color: #fff; }
        .theme-ui .btn:hover:not(:disabled), .theme-ui .timer-btn:hover { background-color: #c960c9; }
        .theme-ui .sentence-display { background-color: #ffe4e1; border-color: #d889d8; }
        .theme-ui .loading-spinner { border-top-color: #d889d8; }
        .theme-ui .nav-btn.active { background-color: #d889d8; }
        
        .theme-ui-mo { background-color: #e0f2f1; }
        .theme-ui-mo .game-container { border-color: #2e8b57; }
        .theme-ui-mo .title, .theme-ui-mo .counter, .theme-ui-mo .timer-container { color: #2e8b57; }
        .theme-ui-mo .btn, .theme-ui-mo .timer-btn { background-color: #2e8b57; border-color: #fff; }
        .theme-ui-mo .btn:hover:not(:disabled), .theme-ui-mo .timer-btn:hover { background-color: #1f6b43; }
        .theme-ui-mo .sentence-display { background-color: #d4edda; border-color: #2e8b57; }
        .theme-ui-mo .loading-spinner { border-top-color: #2e8b57; }
        .theme-ui-mo .nav-btn.active { background-color: #2e8b57; }
        
        .theme-ot { background-color: #fce8a9; }
        .theme-ot .game-container { border-color: #ffcc00; }
        .theme-ot .title, .theme-ot .counter, .theme-ot .timer-container { color: #ffcc00; }
        .theme-ot .btn, .theme-ot .timer-btn { background-color: #ffd700; border-color: #fff; }
        .theme-ot .btn:hover:not(:disabled), .theme-ot .timer-btn:hover { background-color: #ffc200; }
        .theme-ot .sentence-display { background-color: #fffacd; border-color: #ffcc00; }
        .theme-ot .loading-spinner { border-top-color: #ffcc00; }
        .theme-ot .nav-btn.active { background-color: #ffcc00; }

        .theme-at { background-color: #ffcc99; }
        .theme-at .game-container { border-color: #ff9933; }
        .theme-at .title, .theme-at .counter, .theme-at .timer-container { color: #ff9933; }
        .theme-at .btn, .theme-at .timer-btn { background-color: #ff9933; border-color: #fff; }
        .theme-at .btn:hover:not(:disabled), .theme-at .timer-btn:hover { background-color: #ff8c00; }
        .theme-at .sentence-display { background-color: #fff0e0; border-color: #ff9933; }
        .theme-at .loading-spinner { border-top-color: #ff9933; }
        .theme-at .nav-btn.active { background-color: #ff9933; }
        
        .theme-et { background-color: #f0f8ff; }
        .theme-et .game-container { border-color: #4a90e2; }
        .theme-et .title, .theme-et .counter, .theme-et .timer-container { color: #4a90e2; }
        .theme-et .btn, .theme-et .timer-btn { background-color: #4a90e2; border-color: #fff; }
        .theme-et .btn:hover:not(:disabled), .theme-et .timer-btn:hover { background-color: #357bd9; }
        .theme-et .sentence-display { background-color: #c8e6c9; border-color: #4a90e2; }
        .theme-et .loading-spinner { border-top-color: #4a90e2; }
        .theme-et .nav-btn.active { background-color: #4a90e2; }

        .theme-et-hat { background-color: #f7e9f7; } 
        .theme-et-hat .game-container { border-color: #d889d8; }
        .theme-et-hat .title, .theme-et-hat .counter, .theme-et-hat .timer-container { color: #d889d8; }
        .theme-et-hat .btn, .theme-et-hat .timer-btn { background-color: #d889d8; border-color: #fff; }
        .theme-et-hat .btn:hover:not(:disabled), .theme-et-hat .timer-btn:hover { background-color: #c960c9; }
        .theme-et-hat .sentence-display { background-color: #ffe4e1; border-color: #d889d8; }
        .theme-et-hat .loading-spinner { border-top-color: #d889d8; }
        .theme-et-hat .nav-btn.active { background-color: #d889d8; }

        .theme-it { background-color: #e0f2f1; }
        .theme-it .game-container { border-color: #2e8b57; }
        .theme-it .title, .theme-it .counter, .theme-it .timer-container { color: #2e8b57; }
        .theme-it .btn, .theme-it .timer-btn { background-color: #2e8b57; border-color: #fff; }
        .theme-it .btn:hover:not(:disabled), .theme-it .timer-btn:hover { background-color: #1f6b43; }
        .theme-it .sentence-display { background-color: #d4edda; border-color: #2e8b57; }
        .theme-it .loading-spinner { border-top-color: #2e8b57; }
        .theme-it .nav-btn.active { background-color: #2e8b57; }

        .theme-ia { background-color: #ffb6c1; }
        .theme-ia .game-container { border-color: #ff69b4; }
        .theme-ia .title, .theme-ia .counter, .theme-ia .timer-container { color: #ff69b4; }
        .theme-ia .btn, .theme-ia .timer-btn { background-color: #ff69b4; border-color: #fff; }
        .theme-ia .btn:hover:not(:disabled), .theme-ia .timer-btn:hover { background-color: #c71585; }
        .theme-ia .sentence-display { background-color: #ffe4e1; border-color: #ff69b4; }
        .theme-ia .loading-spinner { border-top-color: #ff69b4; }
        .theme-ia .nav-btn.active { background-color: #ff69b4; }

        .theme-uoi { background-color: #fce8a9; }
        .theme-uoi .game-container { border-color: #ffcc00; }
        .theme-uoi .title, .theme-uoi .counter, .theme-uoi .timer-container { color: #ffcc00; }
        .theme-uoi .btn, .theme-uoi .timer-btn { background-color: #ffd700; border-color: #fff; }
        .theme-uoi .btn:hover:not(:disabled), .theme-uoi .timer-btn:hover { background-color: #ffc200; }
        .theme-uoi .sentence-display { background-color: #fffacd; border-color: #ffcc00; }
        .theme-uoi .loading-spinner { border-top-color: #ffcc00; }
        .theme-uoi .nav-btn.active { background-color: #ffcc00; }

        .theme-anh { background-color: #e6e6fa; }
        .theme-anh .game-container { border-color: #9370db; }
        .theme-anh .title, .theme-anh .counter, .theme-anh .timer-container { color: #9370db; }
        .theme-anh .btn, .theme-anh .timer-btn { background-color: #9370db; border-color: #fff; }
        .theme-anh .btn:hover:not(:disabled), .theme-anh .timer-btn:hover { background-color: #8a2be2; }
        .theme-anh .sentence-display { background-color: #f8f8ff; border-color: #9370db; }
        .theme-anh .loading-spinner { border-top-color: #9370db; }
        .theme-anh .nav-btn.active { background-color: #9370db; }

        .theme-ach { background-color: #f0f8ff; }
        .theme-ach .game-container { border-color: #4a90e2; }
        .theme-ach .title, .theme-ach .counter, .theme-ach .timer-container { color: #4a90e2; }
        .theme-ach .btn, .theme-ach .timer-btn { background-color: #4a90e2; border-color: #fff; }
        .theme-ach .btn:hover:not(:disabled), .theme-ach .timer-btn:hover { background-color: #357bd9; }
        .theme-ach .sentence-display { background-color: #c8e6c9; border-color: #4a90e2; }
        .theme-ach .loading-spinner { border-top-color: #4a90e2; }
        .theme-ach .nav-btn.active { background-color: #4a90e2; }

        .theme-ien { background-color: #f7e9f7; }
        .theme-ien .game-container { border-color: #d889d8; }
        .theme-ien .title, .theme-ien .counter, .theme-ien .timer-container { color: #d889d8; }
        .theme-ien .btn, .theme-ien .timer-btn { background-color: #d889d8; border-color: #fff; }
        .theme-ien .btn:hover:not(:disabled), .theme-ien .timer-btn:hover { background-color: #c960c9; }
        .theme-ien .sentence-display { background-color: #ffe4e1; border-color: #d889d8; }
        .theme-ien .loading-spinner { border-top-color: #d889d8; }
        .theme-ien .nav-btn.active { background-color: #d889d8; }

        .theme-uong { background-color: #f0fff0; }
        .theme-uong .game-container { border-color: #228b22; }
        .theme-uong .title, .theme-uong .counter, .theme-uong .timer-container { color: #228b22; }
        .theme-uong .btn, .theme-uong .timer-btn { background-color: #228b22; border-color: #fff; }
        .theme-uong .btn:hover:not(:disabled), .theme-uong .timer-btn:hover { background-color: #176417; }
        .theme-uong .sentence-display { background-color: #c8e6c9; border-color: #228b22; }
        .theme-uong .loading-spinner { border-top-color: #228b22; }
        .theme-uong .nav-btn.active { background-color: #228b22; }

        .theme-uong-mo { background-color: #b0e0e6; }
        .theme-uong-mo .game-container { border-color: #4682b4; }
        .theme-uong-mo .title, .theme-uong-mo .counter, .theme-uong-mo .timer-container { color: #4682b4; }
        .theme-uong-mo .btn, .theme-uong-mo .timer-btn { background-color: #4682b4; border-color: #fff; }
        .theme-uong-mo .btn:hover:not(:disabled), .theme-uong-mo .timer-btn:hover { background-color: #2e648e; }
        .theme-uong-mo .sentence-display { background-color: #add8e6; border-color: #4682b4; }
        .theme-uong-mo .loading-spinner { border-top-color: #4682b4; }
        .theme-uong-mo .nav-btn.active { background-color: #4682b4; }

        .theme-uot { background-color: #fce8e8; }
        .theme-uot .game-container { border-color: #e06666; }
        .theme-uot .title, .theme-uot .counter, .theme-uot .timer-container { color: #e06666; }
        .theme-uot .btn, .theme-uot .timer-btn { background-color: #e06666; border-color: #fff; }
        .theme-uot .btn:hover:not(:disabled), .theme-uot .timer-btn:hover { background-color: #cc3333; }
        .theme-uot .sentence-display { background-color: #fff0f0; border-color: #e06666; }
        .theme-uot .loading-spinner { border-top-color: #e06666; }
        .theme-uot .nav-btn.active { background-color: #e06666; }

        .theme-oai { background-color: #fff8e1; }
        .theme-oai .game-container { border-color: #f99061; }
        .theme-oai .title, .theme-oai .counter, .theme-oai .timer-container { color: #f99061; }
        .theme-oai .btn, .theme-oai .timer-btn { background-color: #f99061; border-color: #fff; }
        .theme-oai .btn:hover:not(:disabled), .theme-oai .timer-btn:hover { background-color: #f47b4d; }
        .theme-oai .sentence-display { background-color: #fffacd; border-color: #f99061; }
        .theme-oai .loading-spinner { border-top-color: #f99061; }
        .theme-oai .nav-btn.active { background-color: #f99061; }
    </style>
</head>
<body>

    <div class="game-container">
        <h1 class="title" id="game-title">Bé Học Vần</h1>
        <div id="nav-container" class="nav-container"></div>
        <div id="sentence-display" class="sentence-display"></div>
        <div id="mic-status" class="text-sm font-semibold text-red-500 mt-2 hidden"></div>
        <div class="controls">
            <button id="prev-btn" class="btn">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M15 19l-7-7 7-7" />
                </svg>
                <span class="btn-text">Lùi lại</span>
            </button>
            <div id="counter" class="counter"></div>
            <button id="next-btn" class="btn">
                <span class="btn-text">Tiến lên</span>
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M9 5l7 7-7 7" />
                </svg>
            </button>
        </div>
        
        <div class="timer-container">
            <span id="timer-display"></span>
            <button id="stop-timer-btn" class="timer-btn">Dừng lại</button>
        </div>

        <div class="record-controls">
            <button id="record-btn" class="record-btn">Ghi âm</button>
            <button id="playback-btn" class="playback-btn" disabled>Nghe lại</button>
        </div>

        <button id="read-aloud-btn" class="read-btn">
            Đọc câu văn (Giọng AI)
        </button>
    </div>

    <div id="loading-overlay" class="loading">
        <div class="loading-spinner"></div>
        <p class="mt-2 text-gray-700 font-bold">Đang tải...</p>
    </div>

    <script type="module">
        import { getAuth, signInAnonymously, signInWithCustomToken } from 'https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js';
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        
        // Constants
        const API_KEY = ""; 
        const API_URL = "https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-tts:generateContent?key=";
        const LOADING_OVERLAY = document.getElementById('loading-overlay');
        const MAX_TIME = 90; // 90 seconds
        
        // Firebase initialization (required by the platform)
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
        const firebaseConfig = JSON.parse(typeof __firebase_config !== 'undefined' ? __firebase_config : '{}');
        const app = initializeApp(firebaseConfig);
        const auth = getAuth(app);
        
        async function authenticate() {
            try {
                const __initial_auth_token = typeof window.__initial_auth_token !== 'undefined' ? window.__initial_auth_token : undefined;
                if (__initial_auth_token) {
                    await signInWithCustomToken(auth, __initial_auth_token);
                } else {
                    await signInAnonymously(auth);
                }
                console.log("Firebase authentication successful.");
            } catch (error) {
                console.error("Firebase authentication failed:", error);
            }
        }
        
        const contentData = [
            { id: "AI", label: "AI", title: "Bé Học Vần AI", themeClass: "theme-ai", sentences: [
                { text: "Bé trai đi hái trái vải.", icons: ["👦", "🍇", "🌳"] },
                { text: "Cái tai nghe bài hát hay.", icons: ["👂", "🎶", "🎤"] },
                { text: "Bé Mai cài bông hoa thật đẹp.", icons: ["👧", "🌸", "💖"] },
                { text: "Ngày mai đi chơi thật vui.", icons: ["📆", "🥳", "🚗"] },
                { text: "Con gà mái nhảy trên bãi cỏ.", icons: ["🐔", "🤸", "🌿"] },
                { text: "Hải cẩu vẫy tai trên bãi cát.", icons: ["🐦", "👂", "🏖️"] },
                { text: "Ngại ngùng làm bạn với bạn mới.", icons: ["😳", "🤝", "👦"] },
                { text: "Bé hái trái dứa toại nguyện.", icons: ["👧", "🍍", "✨"] },
                { text: "Mẹ cài áo cho bé.", icons: ["👩", "👚", "👍"] },
                { text: "Cái tai nghe nhạc thật vui.", icons: ["👂", "🎧", "😊"] },
                { text: "Bé trai đá banh giỏi.", icons: ["👦", "⚽", "🏆"] },
                { text: "Bài hát hay quá.", icons: ["🎶", "🎤", "👍"] },
                { text: "Cá ngài vẫy đuôi.", icons: ["🐟", "🌊", "✨"] },
                { text: "Hải cẩu bay trên biển.", icons: ["🐦", "🌊", "🌬️"] },
                { text: "Ngại ngùng làm sao.", icons: ["😳", "🤫", "😶"] },
                { text: "Bé Mai vẽ cái tai.", icons: ["👧", "🎨", "✍️"] },
                { text: "Cái tai nghe nhạc.", icons: ["👂", "🎧", "🎵"] },
                { text: "Bạn trai của Mai.", icons: ["👦", "👧", "💖"] },
                { text: "Mẹ nói câu hay.", icons: ["👩", "🗣️", "👍"] },
                { text: "Bé trai học bài.", icons: ["👦", "📖", "📚"] }
            ]},
            { id: "OI", label: "OI", title: "Bé Học Vần OI", themeClass: "theme-oi", sentences: [
                { text: "Con voi uống nước bằng vòi.", icons: ["🐘", "💦", "💧"] },
                { text: "Bé hỏi mẹ về những vì sao.", icons: ["👧", "🤔", "⭐"] },
                { text: "Ông nói với tôi về những câu chuyện cổ tích.", icons: ["👴", "📖", "✨"] },
                { text: "Ối giời ơi, con voi to quá.", icons: ["😮", "🐘", "😮"] },
                { text: "Thôi rồi, đi chơi thôi.", icons: ["😊", "🏃", "🤸"] },
                { text: "Cái chổi nhỏ của mẹ.", icons: ["🧹", "🤏", "👩"] },
                { text: "Bé ngồi học bài chăm chỉ.", icons: ["👧", "📚", "✍️"] },
                { text: "Con vòi voi dùng để phun nước.", icons: ["🐘", "💧", "🌊"] },
                { text: "Bé hỏi mẹ về mặt trăng.", icons: ["👧", "🤔", "🌕"] },
                { text: "Tôi hỏi bạn về trò chơi.", icons: ["👦", "❓", "🎮"] },
                { text: "Bạn tôi rất tốt.", icons: ["👫", "👍", "❤️"] },
                { text: "Cái chòi thật nhỏ.", icons: ["🛖", "🤏", "🏡"] },
                { text: "Ông nói với tôi.", icons: ["👴", "🗣️", "👂"] },
                { text: "Mẹ gọi tôi về.", icons: ["👩", "📞", "🏠"] },
                { text: "Bé hỏi mẹ.", icons: ["👧", "🤔", "👩"] },
                { text: "Ối trời ơi, đau quá.", icons: ["😲", "😭", "😖"] },
                { text: "Thôi rồi, ăn bánh đi.", icons: ["😋", "🍰", "🍩"] },
                { text: "Chổi của ba.", icons: ["🧹", "👨", "👍"] },
                { text: "Bé ngồi học bài.", icons: ["👧", "📖", "📚"] },
                { text: "Hỏi ai, hỏi ai.", icons: ["❓", "❓", "🤔"] }
            ]},
            { id: "ỐI", label: "ỐI", title: "Bé Học Vần ÔI", themeClass: "theme-oi-hat", sentences: [
                { text: "Ối, con lợn lười biếng.", icons: ["🐷", "😴", "😮"] },
                { text: "Mẹ phơi quần áo ngoài trời.", icons: ["👩", "👚", "☀️"] },
                { text: "Trái ổi chín thật ngọt.", icons: ["🍐", "😋", "💖"] },
                { text: "Bé cười khúc khích.", icons: ["😂", "😆", "😊"] },
                { text: "Đôi tay mẹ tôi rất khéo.", icons: ["🖐️", "👩", "👍"] },
                { text: "Bé ối lên vì đau bụng.", icons: ["🤢", "😭", "😖"] },
                { text: "Tôm bơi lội trong hồ.", icons: ["🦐", "🏊", "🌊"] },
                { text: "Ối trời, cái gì vậy?", icons: ["😮", "🤔", "❓"] },
                { text: "Cái gói bánh to quá.", icons: ["📦", "🎂", "😮"] },
                { text: "Ôi dối lừa.", icons: ["🤥", "😠", "😤"] },
                { text: "Ối trời ơi, ngã rồi.", icons: ["😮", "😭", "🤕"] },
                { text: "Cái gối mềm mại.", icons: ["🛏️", "😌", "😴"] },
                { text: "Bé lội nước.", icons: ["👦", "🌊", "💧"] },
                { text: "Ối trời, gió to quá.", icons: ["😮", "🌬️", "💨"] },
                { text: "Bé bị hối thúc.", icons: ["🏃", "💨", "⏰"] },
                { text: "Mẹ gói bánh.", icons: ["👩", "🍙", "😋"] },
                { text: "Cái gối ôm của bé.", icons: ["🧸", "😴", "💖"] },
                { text: "Ối, con bò to.", icons: ["😮", "🐄", "🐮"] },
                { text: "Bé lội sông.", icons: ["👦", "🌊", "🐟"] },
                { text: "Đôi mắt của mẹ.", icons: ["👀", "👩", "💖"] }
            ]},
            { id: "ƠI", label: "ƠI", title: "Bé Học Vần ƠI", themeClass: "theme-oi-mo", sentences: [
                { text: "Bạn ơi, đi chơi nào.", icons: ["👋", "🤸", "😊"] },
                { text: "Mẹ ơi, con yêu mẹ.", icons: ["👩", "💖", "❤️"] },
                { text: "Ơ hay, sao bạn ở đây?", icons: ["😮", "👦", "❓"] },
                { text: "Con bơi lơi trên mặt nước.", icons: ["🐟", "🌊", "💧"] },
                { text: "Ơn giời, tớ tới rồi.", icons: ["🙌", "😊", "🏃"] },
                { text: "Ơn nghĩa của cha mẹ.", icons: ["👨‍👩‍👧‍👦", "🙏", "💖"] },
                { text: "Ơ kìa, mèo con của tôi.", icons: ["😺", "👀", "😮"] },
                { text: "Cá lơ lửng trên không trung.", icons: ["🐟", "☁️", "💨"] },
                { text: "Bé ơi, mẹ gọi.", icons: ["👧", "📞", "👩"] },
                { text: "Bạn ơi, ăn kem nào.", icons: ["👫", "🍦", "😋"] },
                { text: "Bố ơi, bố ơi.", icons: ["👨", "🗣️", "📢"] },
                { text: "Ơ hay, bạn đến rồi.", icons: ["😮", "👋", "😊"] },
                { text: "Bé ơi, mẹ thương bé.", icons: ["👧", "💖", "👩"] },
                { text: "Con cá bơi lơ tơ.", icons: ["🐟", "🌊", "💧"] },
                { text: "Con ơi, con về.", icons: ["👩", "🏠", "👋"] },
                { text: "Ơ kìa, mèo con.", icons: ["😺", "👀", "😮"] },
                { text: "Bé ơi, học bài.", icons: ["👧", "📖", "📚"] },
                { text: "Bạn lơ mơ đi đâu.", icons: ["🤔", "🚶", "❓"] },
                { text: "Bé ơi, ăn cơm.", icons: ["👧", "🍚", "🥢"] },
                { text: "Lơ mơ ngủ gật.", icons: ["😴", "😌", "😴"] }
            ]},
            { id: "ON", label: "ON", title: "Bé Học Vần ON", themeClass: "theme-on", sentences: [
                { text: "Con nhện con đang giăng tơ.", icons: ["🕷️", "🕸️", "✨"] },
                { text: "Bố đón con về nhà.", icons: ["👨", "🏡", "👋"] },
                { text: "Bánh bon rất ngon.", icons: ["🍰", "😋", "💖"] },
                { text: "Bé Hòn đi đâu.", icons: ["👧", "🏃", "❓"] },
                { text: "Cái nón của bà.", icons: ["👒", "👵", "👍"] },
                { text: "Gọn gàng, sạch sẽ.", icons: ["🧹", "🧼", "✨"] },
                { text: "Ngon quá đi thôi.", icons: ["😋", "🤤", "👌"] },
                { text: "Bé Lon rất hay.", icons: ["👦", "👍", "👏"] },
                { text: "Bánh bon, bánh ngọt.", icons: ["🍰", "🍬", "🍭"] },
                { text: "Lá non, lá già.", icons: ["🍃", "🍂", "🌳"] },
                { text: "Con mèo con ngoan ngoãn.", icons: ["😺", "😊", "🐾"] },
                { text: "Bố đón con đi học.", icons: ["👨", "🏫", "🚗"] },
                { text: "Con nhím tròn vo.", icons: ["🦔", "⚪", "😊"] },
                { text: "Hòn đá tròn vo.", icons: ["🪨", "⚪", "😮"] },
                { text: "Cái nón lá che nắng.", icons: ["👒", "☀️", "😎"] },
                { text: "Gọn gàng ngăn nắp.", icons: ["🗄️", "🧹", "✨"] },
                { text: "Ngón tay nhỏ xinh.", icons: ["🖐️", "💖", "🤏"] },
                { text: "Bé rất ngon miệng.", icons: ["👦", "😋", "🍲"] },
                { text: "Lá non xanh mơn mởn.", icons: ["🍃", "🌱", "🌿"] },
                { text: "Con lợn béo tròn.", icons: ["🐷", "🐖", "🐷"] }
            ]},
            { id: "AN", label: "AN", title: "Bé Học Vần AN", themeClass: "theme-an", sentences: [
                { text: "Bé an toàn khi qua đường.", icons: ["👦", "🚦", "🚶"] },
                { text: "Gà và cá ăn cám.", icons: ["🐔", "🐟", "🥣"] },
                { text: "Mẹ và bà ở nhà.", icons: ["👩", "👵", "🏡"] },
                { text: "Lan và An đi nhà trẻ.", icons: ["👧", "👦", "🏫"] },
                { text: "Bé An rất ngoan.", icons: ["👧", "👍", "👏"] },
                { text: "Bố an toàn lái xe.", icons: ["👨", "🚗", "👍"] },
                { text: "Hai anh an toàn.", icons: ["👦", "👦", "👍"] },
                { text: "Lan an toàn về nhà.", icons: ["👧", "🏠", "😊"] },
                { text: "Bánh mì ăn ngon.", icons: ["🥖", "😋", "🤤"] },
                { text: "Bạn An ăn quả cam.", icons: ["👦", "🍊", "😋"] },
                { text: "Anh An đi bơi.", icons: ["👦", "🏊", "🌊"] },
                { text: "Bán hàng cho bà.", icons: ["🛍️", "👵", "😊"] },
                { text: "Anh đang ăn bánh.", icons: ["👦", "🍰", "😋"] },
                { text: "Bạn Lan chơi an toàn.", icons: ["👧", "👍", "🤸"] },
                { text: "An toàn là bạn.", icons: ["👍", "❤️", "😊"] },
                { text: "Anh An học giỏi.", icons: ["👦", "📚", "💯"] },
                { text: "Bà An rất tốt.", icons: ["👵", "💖", "👍"] },
                { text: "Bạn Lan ăn quả xoài.", icons: ["👧", "🥭", "😋"] },
                { text: "An toàn giao thông.", icons: ["🚦", "🚗", "🚲"] },
                { text: "Anh An đi chơi.", icons: ["👦", "🥳", "🎉"] }
            ]},
            { id: "UA", label: "UA", title: "Bé Học Vần UA", themeClass: "theme-ua", sentences: [
                { text: "Bạn Rùa chạy đua.", icons: ["🐢", "🏃", "🏁"] },
                { text: "Cua bò lật đật.", icons: ["🦀", "🦀", "➡️"] },
                { text: "Mua cho mẹ một đóa hoa.", icons: ["🛍️", "👩", "💐"] },
                { text: "Lua rua trong gió.", icons: ["🌬️", "🍃", "🍂"] },
                { text: "Con rùa bò chậm.", icons: ["🐢", "🐢", "🚶"] },
                { text: "Ua, thích quá.", icons: ["😍", "🤩", "💖"] },
                { text: "Bé mua quả dứa.", icons: ["👧", "🛍️", "🍍"] },
                { text: "Con rùa ăn dưa.", icons: ["🐢", "🍉", "😋"] },
                { text: "Mua quà cho bé.", icons: ["🎁", "👦", "👧"] },
                { text: "Bé đua xe.", icons: ["👧", "🚗", "💨"] },
                { text: "Đua ngựa, đua xe.", icons: ["🐎", "🚗", "💨"] },
                { text: "Búa của ba.", icons: ["🔨", "👨", "🛠️"] },
                { text: "Lúa đang trổ bông.", icons: ["🌾", "🌱", "🌾"] },
                { text: "Con cua bò nhanh.", icons: ["🦀", "🏃", "💨"] },
                { text: "Hoa mua rất đẹp.", icons: ["🌸", "💖", "😊"] },
                { text: "Mua đồ chơi mới.", icons: ["🛍️", "🧸", "🎁"] },
                { text: "Búa đập đinh.", icons: ["🔨", "🔩", "💥"] },
                { text: "Dứa của bà.", icons: ["🍍", "👵", "🍍"] },
                { text: "Cái rua áo.", icons: ["🧥", "✨", "🎀"] },
                { text: "Rua rua, cua cua.", icons: ["🦀", "🦀", "🦀"] }
            ]},
            { id: "ƯU", label: "ƯU", title: "Bé Học Vần ƯU", themeClass: "theme-uu", sentences: [
                { text: "Cú mèo cúi đầu.", icons: ["🦉", "🙇‍♀️", "🤫"] },
                { text: "Bé được ưu tiên.", icons: ["👧", "👍", "🏆"] },
                { text: "Ưu tư, ưu phiền.", icons: ["😔", "😖", "😭"] },
                { text: "Bạn Ưu rất vui.", icons: ["👦", "😊", "😂"] },
                { text: "Cúi đầu chào cô.", icons: ["🙇‍♀️", "👩‍🏫", "👋"] },
                { text: "Bé Ưu tập viết.", icons: ["👧", "✍️", "📚"] },
                { text: "Ưu điểm của bạn.", icons: ["🌟", "👍", "💖"] },
                { text: "Con cú mèo trên cành cây.", icons: ["🦉", "🌳", "🍃"] },
                { text: "Ưu phiền của mẹ.", icons: ["😔", "👩", "😞"] },
                { text: "Bạn ưu tiên em.", icons: ["🤝", "👦", "👧"] },
                { text: "Ưu tú, ưu tú.", icons: ["✨", "✨", "✨"] },
                { text: "Bé được ưu ái.", icons: ["👧", "💖", "🎁"] },
                { text: "Cúi mặt xuống.", icons: ["🙇‍♂️", "😔", "⬇️"] },
                { text: "Ưu tiên cho người già.", icons: ["👴", "👵", "👍"] },
                { text: "Ưu việt, ưu việt.", icons: ["🏆", "🥇", "✨"] },
                { text: "Con cú ngủ ngày.", icons: ["🦉", "😴", "☀️"] },
                { text: "Ưu phiền đã qua.", icons: ["😔", "➡️", "😊"] },
                { text: "Bé Ưu rất thông minh.", icons: ["👦", "🧠", "💡"] },
                { text: "Cúi xuống nhặt đồ.", icons: ["⬇️", "📦", "🧹"] },
                { text: "Ưu ái với bạn.", icons: ["💖", "🤝", "😊"] }
            ]},
            { id: "ÂN", label: "Ân", title: "Bé Học Vần ÂN", themeClass: "theme-a-mu", sentences: [
                { text: "Ân cần với bạn.", icons: ["🤝", "👦", "😊"] },
                { text: "Ân nhân của bé.", icons: ["😇", "💖", "❤️"] },
                { text: "Bạn Vân hát hay.", icons: ["👧", "🎤", "🎶"] },
                { text: "Lân cận có nhà của bạn.", icons: ["🏡", "👫", "🏠"] },
                { text: "Thật ân cần với mẹ.", icons: ["👩", "💖", "😊"] },
                { text: "Bạn Vân rất hiền.", icons: ["👧", "😊", "💖"] },
                { text: "Văn vẻ của cô.", icons: ["🗣️", "👩‍🏫", "📖"] },
                { text: "Bé Vân vâng lời mẹ.", icons: ["👧", "👍", "👩"] },
                { text: "Ân nghĩa của ba mẹ.", icons: ["👨‍👩‍👧‍👦", "❤️", "💖"] },
                { text: "Thật ân cần.", icons: ["😊", "💖", "🤗"] },
                { text: "Ân cần thăm hỏi.", icons: ["🤝", "👵", "👴"] },
                { text: "Bạn Vân thật tốt.", icons: ["👧", "👍", "😊"] },
                { text: "Ân huệ.", icons: ["🙏", "💖", "✨"] },
                { text: "Vân hát hay.", icons: ["🎶", "🎤", "👍"] },
                { text: "Bé Vân vẽ tranh.", icons: ["👧", "🎨", "🖼️"] },
                { text: "Ân hận, ân hận.", icons: ["😔", "😞", "😭"] },
                { text: "Lân tinh.", icons: ["✨", "🌟", "💫"] },
                { text: "Văn chương thật hay.", icons: ["📖", "✍️", "👍"] },
                { text: "Bạn Vân chăm chỉ.", icons: ["👧", "💪", "📚"] },
                { text: "Ân cần giúp đỡ.", icons: ["🤝", "💖", "😊"] }
            ]},
            { id: "ĂN", label: "ĂN", title: "Bé Học Vần ĂN", themeClass: "theme-a-mo", sentences: [
                { text: "Bé thích ăn bánh.", icons: ["👧", "🍰", "😋"] },
                { text: "Bạn ăn rồi chạy.", icons: ["🏃", "💨", "🤸"] },
                { text: "Ăn cháo đi nào.", icons: ["🥣", "🥄", "😋"] },
                { text: "Mẹ nấu ăn ngon.", icons: ["👩", "🍳", "🍲"] },
                { text: "Bé ăn vạ mẹ.", icons: ["😭", "👩", "😞"] },
                { text: "Ăn dứa thật ngon.", icons: ["🍍", "🤤", "😋"] },
                { text: "Con ốc ăn lá.", icons: ["🐌", "🍃", "🌿"] },
                { text: "Ông bà ăn bánh quy.", icons: ["👴", "👵", "🍪"] },
                { text: "Ăn sáng cho chắc dạ.", icons: ["🍳", "💪", "👍"] },
                { text: "Ăn xong rồi đi ngủ.", icons: ["😴", "🛌", "😌"] },
                { text: "Ăn no rồi chơi.", icons: ["😋", "🍔", "🤸"] },
                { text: "Bạn ăn cơm ngon.", icons: ["👦", "🍚", "😋"] },
                { text: "Ăn bánh rồi uống sữa.", icons: ["🍰", "🥛", "🤤"] },
                { text: "Ăn trái cây.", icons: ["🍎", "🍊", "🍇"] },
                { text: "Bé ăn vạ.", icons: ["👧", "😭", "😤"] },
                { text: "Ăn dặm để lớn.", icons: ["👶", "💪", "🌱"] },
                { text: "Ăn uống đúng giờ.", icons: ["⏰", "😋", "👍"] },
                { text: "Bạn ốc sên ăn lá.", icons: ["🐌", "🍃", "🥬"] },
                { text: "Ăn nhiều bánh ngọt.", icons: ["🍰", "😋", "🤤"] },
                { text: "Bạn ăn gì vậy.", icons: ["👦", "❓", "🤔"] }
            ]},
            { id: "ÔI", label: "ÔI", title: "Bé Học Vần ÔI", themeClass: "theme-oi-hat", sentences: [
                { text: "Đôi tay mẹ tôi rất khéo.", icons: ["🖐️", "👩", "👍"] },
                { text: "Nước sôi sùng sục.", icons: ["💧", "🔥", "💨"] },
                { text: "Lội nước trên ao.", icons: ["👦", "🌊", "🚶"] },
                { text: "Gối đầu trên tay mẹ.", icons: ["👩", "😴", "💖"] },
                { text: "Hối hả đi học.", icons: ["🏃", "💨", "🏫"] },
                { text: "Gói quà cho bạn.", icons: ["🎁", "🤝", "🎉"] },
                { text: "Cối xay gió.", icons: ["🛕", "🌬️", "💨"] },
                { text: "Khung cửi dệt vải.", icons: ["🧺", "🧵", "👕"] },
                { text: "Ối, con bò to.", icons: ["😮", "🐄", "🐮"] },
                { text: "Trái ổi chín thật ngọt.", icons: ["🍐", "😋", "💖"] },
                { text: "Bé lội nước.", icons: ["👦", "🌊", "💧"] },
                { text: "Ối trời ơi, ngã rồi.", icons: ["😮", "😭", "🤕"] },
                { text: "Gối đầu.", icons: ["🛏️", "😴", "😌"] },
                { text: "Nồi cơm nóng.", icons: ["🍚", "🔥", "🍲"] },
                { text: "Bé hối hả.", icons: ["👦", "🏃", "💨"] },
                { text: "Gói bánh chưng.", icons: ["🌿", "🍙", "😋"] },
                { text: "Cối đá.", icons: ["🪨", "🗿", "🔨"] },
                { text: "Khung cửi.", icons: ["🧺", "🧵", "⚙️"] },
                { text: "Ôi trời ơi.", icons: ["😮", "😲", "😱"] },
                { text: "Trôi đi nhanh.", icons: ["🌊", "💨", "➡️"] }
            ]},
            { id: "ƠI", label: "ƠI", title: "Bé Học Vần ƠI", themeClass: "theme-oi-mo", sentences: [
                { text: "Mẹ ơi, con đi học.", icons: ["👩", "👧", "🏫"] },
                { text: "Bà ơi, cháu về.", icons: ["👵", "👋", "🏡"] },
                { text: "Đứng chơi, ngồi chơi.", icons: ["🤸", "🪑", "😊"] },
                { text: "Trái bưởi da xanh.", icons: ["🍊", "🟢", "😋"] },
                { text: "Bé chơi trò bơi.", icons: ["👧", "🏊", "💧"] },
                { text: "Lười biếng không tốt.", icons: ["😴", "😠", "👎"] },
                { text: "Mời bạn vào nhà.", icons: ["👋", "🏡", "👦"] },
                { text: "Gọi tôi đi chơi.", icons: ["📞", "👦", "🤸"] },
                { text: "Bé ơi, mẹ gọi.", icons: ["👧", "👩", "📢"] },
                { text: "Ơ hay, bạn đến rồi.", icons: ["😮", "👋", "😊"] },
                { text: "Bố ơi, bố ơi.", icons: ["👨", "🗣️", "📢"] },
                { text: "Ơ kìa, mèo con.", icons: ["😺", "👀", "😮"] },
                { text: "Bé ơi, học bài.", icons: ["👧", "📖", "📚"] },
                { text: "Bạn lơ mơ đi đâu.", icons: ["🤔", "🚶", "❓"] },
                { text: "Bé ơi, ăn cơm.", icons: ["👧", "🍚", "🥢"] },
                { text: "Lơ mơ ngủ gật.", icons: ["😴", "😌", "😴"] },
                { text: "Mời bạn ăn kẹo.", icons: ["🍬", "🍭", "😊"] },
                { text: "Lười biếng thì không vui.", icons: ["😴", "😔", "😖"] },
                { text: "Ơi, mẹ đã về.", icons: ["👩", "🏠", "😊"] },
                { text: "Mời bạn chơi.", icons: ["🤝", "🤸", "😂"] }
            ]},
            { id: "EN", label: "EN", title: "Bé Học Vần EN", themeClass: "theme-en", sentences: [
                { text: "Con ếch kêu ền ền.", icons: ["🐸", "🔊", "🎶"] },
                { text: "Bé thổi kèn thật to.", icons: ["🎺", "👦", "📢"] },
                { text: "Lên đền rồi đi về.", icons: ["🏛️", "👋", "🏡"] },
                { text: "Rèn luyện sức khỏe.", icons: ["💪", "🤸", "🏋️"] },
                { text: "Bánh chưng, bánh tét.", icons: ["🍙", "🍙", "😋"] },
                { text: "Chân của con voi.", icons: ["🐘", "🦶", "🦵"] },
                { text: "Đèn đường buổi tối.", icons: ["💡", "🌃", "✨"] },
                { text: "Bạn Tên rất giỏi.", icons: ["👦", "👍", "🏆"] },
                { text: "Em thổi kèn.", icons: ["👧", "🎺", "🎶"] },
                { text: "Con nhện giăng tơ.", icons: ["🕷️", "🕸️", "✨"] },
                { text: "Em ăn kem.", icons: ["👧", "🍦", "😋"] },
                { text: "Lên lớp.", icons: ["🏫", "🚶", "⬆️"] },
                { text: "Rèn luyện.", icons: ["💪", "🏋️", "👍"] },
                { text: "Đèn pin.", icons: ["🔦", "💡", "✨"] },
                { text: "Tên tôi là An.", icons: ["📝", "👦", "👧"] },
                { text: "Bánh tét.", icons: ["🍙", "😋", "🤤"] },
                { text: "Chân gà.", icons: ["🐔", "🦶", "🦵"] },
                { text: "Đèn lồng.", icons: ["🏮", "💡", "✨"] },
                { text: "Lên xe.", icons: ["🚗", "⬆️", "💨"] },
                { text: "Lên bờ.", icons: ["🌊", "🚶", "🏞️"] }
            ]},
            { id: "ÊN", label: "ÊN", title: "Bé Học Vần ÊN", themeClass: "theme-en-hat", sentences: [
                { text: "Bé mến cô giáo.", icons: ["👧", "💖", "👩‍🏫"] },
                { text: "Cái ghế gỗ của ba.", icons: ["🪑", "🪵", "👨"] },
                { text: "Lên trên cầu thang.", icons: ["⬆️", "🪜", "🚶"] },
                { text: "Ghế đẩu rất nhỏ.", icons: ["🪑", "🤏", "😊"] },
                { text: "Thế là bé lên giường.", icons: ["👧", "🛏️", "😴"] },
                { text: "Cánh chim bay trên trời.", icons: ["🐦", "🌬️", "☁️"] },
                { text: "Bé chê dở.", icons: ["👧", "👎", "😠"] },
                { text: "Sẽ đến lúc ăn bánh.", icons: ["⏰", "🍰", "😋"] },
                { text: "Bé lên thuyền.", icons: ["👧", "⛵", "🌊"] },
                { text: "Ghế thật êm.", icons: ["🪑", "😌", "👍"] },
                { text: "Bé mến yêu cô.", icons: ["💖", "👩‍🏫", "😊"] },
                { text: "Ếch ngồi trên bàn.", icons: ["🐸", "🪑", "👀"] },
                { text: "Ghế da mềm mại.", icons: ["🪑", "😌", "✨"] },
                { text: "Thuyền buồm đang lên.", icons: ["⛵", "⬆️", "🌊"] },
                { text: "Bé chê kem dở.", icons: ["👧", "🍦", "😖"] },
                { text: "Bé mến cô giáo.", icons: ["💖", "👩‍🏫", "😊"] },
                { text: "Ghế đẩu.", icons: ["🪑", "🪑", "🪑"] },
                { text: "Sẽ có bánh.", icons: ["🍰", "😋", "🤤"] },
                { text: "Bé chê.", icons: ["👧", "👎", "😠"] },
                { text: "Ghế gỗ.", icons: ["🪑", "🪵", "🌳"] }
            ]},
            { id: "AY", label: "AY", title: "Bé Học Vần AY", themeClass: "theme-ay", sentences: [
                { text: "Ngày mai đi học.", icons: ["📆", "🏫", "🎒"] },
                { text: "Máy bay bay thật cao.", icons: ["✈️", "☁️", "⬆️"] },
                { text: "Làm bài tập ngay.", icons: ["✍️", "📚", "⏰"] },
                { text: "Cái dây thun của mẹ.", icons: [" elastic band", "🧵", "👩"] },
                { text: "Bé May hay hát.", icons: ["👧", "🎶", "🎤"] },
                { text: "Giúp tôi cái tay.", icons: ["🤝", "👦", "🖐️"] },
                { text: "Cái máy bay thật to.", icons: ["✈️", "😮", "✨"] },
                { text: "May vá quần áo.", icons: ["🧵", "👚", "🪡"] },
                { text: "Tay nắm tay.", icons: ["🤝", "❤️", "😊"] },
                { text: "Ngày hôm nay thật vui.", icons: ["📆", "☀️", "🥳"] },
                { text: "Bé hay hát.", icons: ["👧", "🎶", "🎤"] },
                { text: "Tay trái, tay phải.", icons: ["🖐️", "🖐️", "✋"] },
                { text: "May áo cho búp bê.", icons: ["🧵", "👗", "🧸"] },
                { text: "Ngày ngày đi học.", icons: ["📆", "🏫", "🎒"] },
                { text: "Máy bay bay.", icons: ["✈️", "💨", "☁️"] },
                { text: "Bé hay cười.", icons: ["👧", "😂", "😊"] },
                { text: "Tay cầm bút.", icons: ["🖐️", "✍️", "✏️"] },
                { text: "May đồ.", icons: ["🧵", "👚", "👕"] },
                { text: "Ngày đi chơi.", icons: ["📆", "🥳", "🎉"] },
                { text: "Bạn hay hát.", icons: ["👦", "🎶", "🎤"] }
            ]},
            { id: "ÂY", label: "ÂY", title: "Bé Học Vần ÂY", themeClass: "theme-ay-hat", sentences: [
                { text: "Bé thấy con gấu.", icons: ["👧", "👀", "🐻"] },
                { text: "Cái cây rất cao.", icons: ["🌳", "⬆️", "🌳"] },
                { text: "Đây là nhà tôi.", icons: ["👉", "🏡", "🏠"] },
                { text: "Bé lấy chiếc giày.", icons: ["👧", "👟", "🛍️"] },
                { text: "Dậy sớm tập thể dục.", icons: ["⏰", "🤸", "💪"] },
                { text: "Bảy sắc cầu vồng.", icons: ["🌈", "🌈", "🌈"] },
                { text: "Nắm lấy tay bạn.", icons: ["🤝", "👦", "👧"] },
                { text: "Thấy bạn, bé cười.", icons: ["👀", "😊", "😂"] },
                { text: "Cây to, cây nhỏ.", icons: ["🌳", "🌳", "🌲"] },
                { text: "Giúp mẹ cấy lúa.", icons: ["🌾", "👩", "👨‍🌾"] },
                { text: "Đậy nắp hộp sữa.", icons: ["🥛", "📦", "👍"] },
                { text: "Lấy sách, lấy vở.", icons: ["📖", "📚", "✍️"] },
                { text: "Cái cây xanh mướt.", icons: ["🌳", "🟢", "🌿"] },
                { text: "Mẹ lấy quả cam.", icons: ["👩", "🍊", "😋"] },
                { text: "Thấy bạn tôi.", icons: ["👀", "👦", "👧"] },
                { text: "Bé lấy quả táo.", icons: ["👧", "🍎", "😋"] },
                { text: "Cây dừa cao.", icons: ["🌴", "⬆️", "🌳"] },
                { text: "Mẹ lấy đồ chơi.", icons: ["👩", "🧸", "🎁"] },
                { text: "Bé cấy lúa.", icons: ["👧", "🌾", "🚜"] },
                { text: "Lấy đồ cho em.", icons: ["🛍️", "👦", "👧"] }
            ]},
            { id: "OM", label: "OM", title: "Bé Học Vần OM", themeClass: "theme-om", sentences: [
                { text: "Con bướm bay trên đóm hoa.", icons: ["🦋", "💐", "🌸"] },
                { text: "Cơm nóng ăn ngon.", icons: ["🍚", "🔥", "😋"] },
                { text: "Bé ôm gấu bông.", icons: ["👧", "🧸", "🤗"] },
                { text: "Con tôm bơi lội.", icons: ["🦐", "🏊", "🌊"] },
                { text: "Chiếc rơm khô.", icons: ["🌾", "🌾", "🌾"] },
                { text: "Cơm của mẹ.", icons: ["🍚", "👩", "💖"] },
                { text: "Bé ôm mẹ thật chặt.", icons: ["👧", "👩", "🤗"] },
                { text: "Tôm tép của ba.", icons: ["🦐", "👨", "😋"] },
                { text: "Đốm lửa nhỏ.", icons: ["🔥", "🤏", "✨"] },
                { text: "Con tôm màu đỏ.", icons: ["🦐", "🔴", "🦞"] },
                { text: "Chị Sương bơi lội.", icons: ["👧", "🏊", "💧"] },
                { text: "Con đom đóm.", icons: ["✨", "🌟", "💡"] },
                { text: "Cơm của con.", icons: ["🍚", "👦", "👧"] },
                { text: "Bé ôm bạn.", icons: ["👧", "👦", "🤝"] },
                { text: "Con tôm càng to.", icons: ["🦐", "😮", "💪"] },
                { text: "Rơm rạ.", icons: ["🌾", "🌾", "🌾"] },
                { text: "Đốm lửa.", icons: ["🔥", "✨", "💡"] },
                { text: "Ôm mẹ.", icons: ["🤗", "👩", "💖"] },
                { text: "Con tôm nhảy.", icons: ["🦐", "🤸", "💨"] },
                { text: "Rơm rạ khô.", icons: ["🌾", "☀️", "🌾"] }
            ]},
            { id: "AM", label: "AM", title: "Bé Học Vần AM", themeClass: "theme-am", sentences: [
                { text: "Quả cam, quả chanh.", icons: ["🍊", "🍋", "🍏"] },
                { text: "Mẹ mang chiếc cặp.", icons: ["👩", "👜", "💼"] },
                { text: "Bé học bài chăm chỉ.", icons: ["👧", "📖", "✍️"] },
                { text: "Chân chậm, tay cầm.", icons: ["🚶", "🖐️", "🚶"] },
                { text: "Đêm rằm thật sáng.", icons: ["🌕", "🌃", "✨"] },
                { text: "Nấm rơm rất ngon.", icons: ["🍄", "😋", "🤤"] },
                { text: "Bạn làm bài tập.", icons: ["👦", "📚", "✍️"] },
                { text: "Cái cặp sách của bạn.", icons: ["🎒", "👦", "👧"] },
                { text: "Làm lồng đèn.", icons: ["🏮", "💡", "💖"] },
                { text: "Bạn chăm ngoan.", icons: ["👍", "😊", "💖"] },
                { text: "Quả cam.", icons: ["🍊", "😋", "🍊"] },
                { text: "Cái cặp.", icons: ["🎒", "📚", "✏️"] },
                { text: "Làm bài.", icons: ["✍️", "📖", "📚"] },
                { text: "Lá thăm.", icons: ["🎲", "🍀", "👍"] },
                { text: "Rằm trung thu.", icons: ["🏮", "🌕", "🎉"] },
                { text: "Cây cam.", icons: ["🌳", "🍊", "🌱"] },
                { text: "Con cám.", icons: ["🌾", "🐟", "🍚"] },
                { text: "Mẹ làm bánh.", icons: ["👩", "🍰", "😋"] },
                { text: "Cái cặp to.", icons: ["🎒", "😮", "💖"] },
                { text: "Bạn An chăm.", icons: ["👦", "👍", "😊"] }
            ]},
            { id: "AU", label: "AU", title: "Bé Học Vần AU", themeClass: "theme-au", sentences: [
                { text: "Cái rau cải thật ngon.", icons: ["🥬", "😋", "🤤"] },
                { text: "Bạn Rau rất hay.", icons: ["👦", "👍", "👏"] },
                { text: "Con tẩu bay đi đâu.", icons: ["✈️", "❓", "🤔"] },
                { text: "Bé đau bụng rồi.", icons: ["👧", "😭", "😖"] },
                { text: "Mẹ nấu ăn ngon.", icons: ["👩", "🍳", "🍲"] },
                { text: "Con râu con rể.", icons: ["👨‍🦱", "👩‍🦱", "👨‍👩‍👧‍👦"] },
                { text: "Đau rồi khóc đi.", icons: ["😭", "😥", "😔"] },
                { text: "Cháu rất hiền.", icons: ["👦", "😊", "💖"] },
                { text: "Nhà cháu có nhiều đồ chơi.", icons: ["🏡", "🧸", "🎁"] },
                { text: "Sáu tuổi đi học.", icons: ["👧", "📚", "🏫"] },
                { text: "Rau cải.", icons: ["🥬", "🥗", "😋"] },
                { text: "Nấu cơm.", icons: ["🍚", "🍳", "🍲"] },
                { text: "Bé đau.", icons: ["👧", "😭", "😖"] },
                { text: "Bạn đau.", icons: ["👦", "😭", "😖"] },
                { text: "Cháu ngoan.", icons: ["👦", "👍", "👏"] },
                { text: "Sáu quả cam.", icons: ["6️⃣", "🍊", "🍊"] },
                { text: "Mẹ nấu cháo.", icons: ["👩", "🥣", "😋"] },
                { text: "Rau muống.", icons: ["🥬", "😋", "🤤"] },
                { text: "Cháu bé.", icons: ["👶", "🧒", "👧"] },
                { text: "Đau chân.", icons: ["🦶", "🤕", "😭"] }
            ]},
            { id: "ÂU", label: "ÂU", title: "Bé Học Vần ÂU", themeClass: "theme-au-hat", sentences: [
                { text: "Con sâu ăn lá.", icons: ["🐛", "🍃", "🌿"] },
                { text: "Chị Sâu rất sâu sắc.", icons: ["👧", "🧠", "💡"] },
                { text: "Vào vườn, hái rau.", icons: ["🏡", "🥬", "🫙"] },
                { text: "Cầu thủ ghi bàn.", icons: ["⚽", "🏆", "🏃"] },
                { text: "Cái cầu rất cao.", icons: ["🌉", "⬆️", "☁️"] },
                { text: "Bé lầu bầu.", icons: ["👦", "😠", "🗣️"] },
                { text: "Nơi sâu nhất.", icons: ["🌊", "⬇️", "🤿"] },
                { text: "Đấu võ, đấu kiếm.", icons: ["🥋", "⚔️", "💪"] },
                { text: "Bé sầu vì bị điểm kém.", icons: ["👧", "😔", "😭"] },
                { text: "Bạn Sầu rất tốt.", icons: ["👦", "👍", "💖"] },
                { text: "Con sâu.", icons: ["🐛", "🪱", "🌱"] },
                { text: "Cây cầu.", icons: ["🌉", "🌉", "🌉"] },
                { text: "Cầu thủ.", icons: ["⚽", "🏆", "🏃"] },
                { text: "Đấu tranh.", icons: ["💪", "💪", "👊"] },
                { text: "Lầu cao.", icons: ["🏢", "⬆️", "🏠"] },
                { text: "Sâu.", icons: ["🐛", "🪱", "🪱"] },
                { text: "Vào trong.", icons: ["➡️", "🚶", "🏠"] },
                { text: "Bé sầu.", icons: ["👧", "😔", "😞"] },
                { text: "Cầu nguyện.", icons: ["🙏", "💖", "✨"] },
                { text: "Lầu bầu.", icons: ["😠", "😤", "🗣️"] }
            ]},
            { id: "UÔN", label: "UÔN", title: "Bé Học Vần UÔN", themeClass: "theme-uon", sentences: [
                { text: "Cuốn sách của bé.", icons: ["📖", "📚", "💖"] },
                { text: "Vườn rau xanh mướt.", icons: ["🏡", "🥬", "🌱"] },
                { text: "Bạn Duân thật giỏi.", icons: ["👦", "🏆", "👏"] },
                { text: "Uôn uôn, uôn uôn.", icons: ["🎶", "🎵", "🔊"] },
                { text: "Buồn bã, buồn rầu.", icons: ["😔", "😞", "😭"] },
                { text: "Vườn hoa hồng.", icons: ["🌹", "🌸", "💐"] },
                { text: "Bé cuộn mình ngủ.", icons: ["👧", "🛌", "😴"] },
                { text: "Bạn Luân rất ngoan.", icons: ["👦", "👍", "😊"] },
                { text: "Cuốn vở của ba.", icons: ["📖", "👨", "📚"] },
                { text: "Buồn ngủ, buồn ngủ.", icons: ["😴", "😌", "😴"] },
                { text: "Cuốn sách.", icons: ["📖", "📚", "📚"] },
                { text: "Vườn cây.", icons: ["🌳", "🌲", "🌳"] },
                { text: "Buồn ngủ.", icons: ["😴", "😔", "😴"] },
                { text: "Luân chuyển.", icons: ["🔄", "🔄", "🔄"] },
                { text: "Vườn táo.", icons: ["🍎", "🌳", "🍏"] },
                { text: "Bạn Duân.", icons: ["👦", "👧", "🧑"] },
                { text: "Cuộn chỉ.", icons: ["🧵", "🧶", "🧵"] },
                { text: "Luân phiên.", icons: ["🔄", "🔄", "🔄"] },
                { text: "Buồn bã.", icons: ["😔", "😞", "😭"] },
                { text: "Cuộn giấy.", icons: ["📄", "📜", "📜"] }
            ]},
            { id: "ƯƠN", label: "ƯƠN", title: "Bé Học Vần ƯƠN", themeClass: "theme-uon-mo", sentences: [
                { text: "Con lươn trườn trên bùn.", icons: ["🐍", "💩", "🌿"] },
                { text: "Cánh vườn ươm cây.", icons: ["🌳", "🌱", "🌿"] },
                { text: "Bé ươn lên để hái quả.", icons: ["👦", "🍇", "⬆️"] },
                { text: "Ươn ươn, ươn ươn.", icons: ["🎶", "🎵", "🔊"] },
                { text: "Buồn bã, buồn rầu.", icons: ["😔", "😞", "😭"] },
                { text: "Vườn rau xanh mướt.", icons: ["🏡", "🥬", "🌱"] },
                { text: "Lườn lượn qua lại.", icons: ["🚶", "🔄", "🔄"] },
                { text: "Bé thích lượn vòng.", icons: ["👧", "🔄", "💨"] },
                { text: "Vườn cây của ông.", icons: ["🌳", "👴", "🌿"] },
                { text: "Ươm mầm xanh.", icons: ["🌱", "🌿", "💧"] },
                { text: "Lươn trườn.", icons: ["🐍", "🐍", "💨"] },
                { text: "Ươm mầm.", icons: ["🌱", "🌿", "💧"] },
                { text: "Buồn nôn.", icons: ["🤢", "🤮", "😖"] },
                { text: "Vườn rau.", icons: ["🏡", "🥬", "🥗"] },
                { text: "Lươn.", icons: ["🐍", "🐟", "🐠"] },
                { text: "Vườn cây.", icons: ["🌳", "🌿", "🌲"] },
                { text: "Ươm.", icons: ["🌱", "💧", "☀️"] },
                { text: "Lượn.", icons: ["🔄", "🔄", "🔄"] },
                { text: "Lươn lẹo.", icons: ["🤥", "🤫", "🤥"] },
                { text: "Ươn.", icons: ["🗣️", "🎵", "🎶"] }
            ]},
            { id: "ÔN", label: "ÔN", title: "Bé Học Vần ÔN", themeClass: "theme-on-hat", sentences: [
                { text: "Con chồn hòn chốn.", icons: ["🦊", "🏃", "💨"] },
                { text: "Tôn trọng người lớn.", icons: ["👍", "👴", "👵"] },
                { text: "Bé ôn bài thật giỏi.", icons: ["👧", "📖", "✍️"] },
                { text: "Bạn Tôn rất thông minh.", icons: ["👦", "🧠", "💡"] },
                { text: "Bé chồn đi chơi.", icons: ["🦊", "🏃", "🤸"] },
                { text: "Ôn tập mỗi ngày.", icons: ["📚", "✍️", "📖"] },
                { text: "Ôn hòa với bạn bè.", icons: ["🤝", "😊", "💖"] },
                { text: "Chồn chồn.", icons: ["🦊", "🦊", "🦊"] },
                { text: "Tôn trọng.", icons: ["👍", "👏", "💖"] },
                { text: "Ôn bài.", icons: ["📚", "📖", "✍️"] },
                { text: "Bạn Tôn.", icons: ["👦", "👧", "🧑"] },
                { text: "Chồn.", icons: ["🦊", "🦊", "🦊"] },
                { text: "Tôn vinh.", icons: ["🏆", "🥇", "✨"] },
                { text: "Ôn hòa.", icons: ["😊", "😌", "💖"] },
                { text: "Tôn vinh.", icons: ["🏆", "🥇", "✨"] },
                { text: "Chồn.", icons: ["🦊", "🦊", "🦊"] },
                { text: "Tôn.", icons: ["👦", "👧", "🧑"] },
                { text: "Ôn.", icons: ["📚", "📖", "✍️"] },
                { text: "Chồn.", icons: ["🦊", "🦊", "🦊"] },
                { text: "Tôn trọng.", icons: ["👍", "👏", "💖"] }
            ]},
            { id: "ƠN", label: "ƠN", title: "Bé Học Vần ƠN", themeClass: "theme-on-mo", sentences: [
                { text: "Ơn giời, cậu đây rồi.", icons: ["🙏", "😊", "🏃"] },
                { text: "Con sơn ca hót hay.", icons: ["🐦", "🎶", "🎤"] },
                { text: "Bé rất biết ơn.", icons: ["👧", "🙏", "💖"] },
                { text: "Sơn móng tay cho mẹ.", icons: ["💅", "👩", "✨"] },
                { text: "Bé nhởn nhơ chơi.", icons: ["👦", "🤸", "😊"] },
                { text: "Ơn nghĩa của mẹ.", icons: ["👩", "💖", "🙏"] },
                { text: "Sơn tường nhà.", icons: ["🏠", "🎨", "🧑‍🎨"] },
                { text: "ơn giời.", icons: ["🙏", "😊", "💖"] },
                { text: "Sơn ca.", icons: ["🐦", "🎶", "🎤"] },
                { text: "Bé biết ơn.", icons: ["👧", "🙏", "💖"] },
                { text: "Sơn.", icons: ["🎨", "🖌️", "🧑‍🎨"] },
                { text: "Ơn nghĩa.", icons: ["❤️", "🙏", "💖"] },
                { text: "Nhởn nhơ.", icons: ["😊", " carefree", "✨"] },
                { text: "Sơn ca hát.", icons: ["🐦", "🎶", "🎤"] },
                { text: "Ơn.", icons: ["🙏", "💖", "😊"] },
                { text: "Sơn móng.", icons: ["💅", "💅", "💅"] },
                { text: "Sơn màu.", icons: ["🎨", "🖌️", "🎨"] },
                { text: "Ơn.", icons: ["🙏", "💖", "😊"] },
                { text: "Sơn ca.", icons: ["🐦", "🎶", "🎤"] },
                { text: "Biết ơn.", icons: ["🙏", "💖", "😊"] }
            ]},
            { id: "EO", label: "EO", title: "Bé Học Vần EO", themeClass: "theme-eo", sentences: [
                { text: "Con mèo ngoèo đuôi.", icons: ["😺", "🐈", "💨"] },
                { text: "Bé nheo mắt cười.", icons: ["👦", "😊", "😂"] },
                { text: "Con chim hót reo.", icons: ["🐦", "🎶", "🎤"] },
                { text: "Cái kẹo thật ngọt.", icons: ["🍭", "🍬", "😋"] },
                { text: "Bé đi dẻo chân.", icons: ["👧", "🚶", "🚶"] },
                { text: "Leo cây hái quả.", icons: ["🌳", "🍇", "🍎"] },
                { text: "Cái kèo của nhà.", icons: ["🏠", "🪵", "🔨"] },
                { text: "Bé reo hò.", icons: ["👦", "📢", "🎉"] },
                { text: "Con mèo kêu meo meo.", icons: ["😺", "🐈", "🔊"] },
                { text: "Bé nheo mắt.", icons: ["👦", "👀", "😊"] },
                { text: "Reo hò.", icons: ["📢", "🎉", "🥳"] },
                { text: "Kẹo.", icons: ["🍬", "🍭", "😋"] },
                { text: "Leo trèo.", icons: ["🧗", "🌳", "🤸"] },
                { text: "Kèo.", icons: ["🔨", "🪵", "🏠"] },
                { text: "Reo hò.", icons: ["📢", "🎉", "🥳"] },
                { text: "Mèo.", icons: ["😺", "🐈", "🐾"] },
                { text: "Nheo.", icons: ["👀", "🤫", "😶"] },
                { text: "Reo hò.", icons: ["📢", "🎉", "🥳"] },
                { text: "Kẹo.", icons: ["🍬", "🍭", "😋"] },
                { text: "Leo.", icons: ["🧗", "🌳", "🤸"] }
            ]},
            { id: "AO", label: "AO", title: "Bé Học Vần AO", themeClass: "theme-ao", sentences: [
                { text: "Quả táo màu đỏ.", icons: ["🍎", "🔴", "😋"] },
                { text: "Áo len của bé.", icons: ["👚", "🧶", "🧥"] },
                { text: "Ao cá của ông.", icons: ["🐟", "👴", "💧"] },
                { text: "Bé táo tợn.", icons: ["👦", "😠", "😤"] },
                { text: "Học lao động.", icons: ["👩‍🌾", "🔨", "🪚"] },
                { text: "Cái áo của ba.", icons: ["👚", "👨", "👕"] },
                { text: "Bạn ấy học thật giỏi.", icons: ["👦", "📚", "💯"] },
                { text: "Bé xoa đầu bạn.", icons: ["👧", "🤝", "👦"] },
                { text: "Ao của làng.", icons: ["💧", "🏡", "🌊"] },
                { text: "Bạn lao động.", icons: ["👩‍🌾", "👨‍🏭", "🧑‍🔧"] },
                { text: "Quả táo.", icons: ["🍎", "🍏", "🍎"] },
                { text: "Cái áo.", icons: ["👚", "👕", "🧥"] },
                { text: "Cái ao.", icons: ["💧", "🌊", "💧"] },
                { text: "Lao động.", icons: ["💪", "🏋️", "🏃"] },
                { text: "Ao cá.", icons: ["🐟", "🐟", "🐟"] },
                { text: "Áo.", icons: ["👚", "👕", "🧥"] },
                { text: "Lao.", icons: ["💪", "🏋️", "🏃"] },
                { text: "Ao.", icons: ["💧", "🌊", "💧"] },
                { text: "Táo.", icons: ["🍎", "🍏", "🍎"] },
                { text: "Lao động.", icons: ["💪", "🏋️", "🏃"] }
            ]},
            { id: "ONG", label: "ONG", title: "Bé Học Vần ONG", themeClass: "theme-ong", sentences: [
                { text: "Con ong chăm chỉ làm mật.", icons: ["🐝", "🍯", "😋"] },
                { text: "Bé rất thích thổi bong bóng.", icons: ["👧", "🎈", "🎈"] },
                { text: "Con công xòe đuôi.", icons: ["🦚", "✨", "👑"] },
                { text: "Ông bà rất tốt.", icons: ["👴", "👵", "💖"] },
                { text: "Bong bóng bay lên trời.", icons: ["🎈", "☁️", "⬆️"] },
                { text: "Con ong bay đi đâu.", icons: ["🐝", "❓", "🤔"] },
                { text: "Con công có nhiều màu.", icons: ["🦚", "🌈", "✨"] },
                { text: "Ông già Noel.", icons: ["🎅", "🎁", "🎄"] },
                { text: "Bé rất thích thổi bong bóng.", icons: ["👧", "🎈", "😂"] },
                { text: "Con ong bay.", icons: ["🐝", "💨", "✨"] },
                { text: "Con ong.", icons: ["🐝", "🐝", "🐝"] },
                { text: "Bong bóng.", icons: ["🎈", "🎈", "🎈"] },
                { text: "Con công.", icons: ["🦚", "🦚", "🦚"] },
                { text: "Ông.", icons: ["👴", "👨‍🦳", "🧓"] },
                { text: "Ong mật.", icons: ["🍯", "🐝", "😋"] },
                { text: "Bong bóng bay.", icons: ["🎈", "☁️", "⬆️"] },
                { text: "Con công.", icons: ["🦚", "🦚", "🦚"] },
                { text: "Ông già.", icons: ["👴", "👨‍🦳", "🧓"] },
                { text: "Bong bóng.", icons: ["🎈", "🎈", "🎈"] },
                { text: "Con ong.", icons: ["🐝", "🐝", "🐝"] }
            ]},
            { id: "ÔNG", label: "ÔNG", title: "Bé Học Vần ÔNG", themeClass: "theme-ong-hat", sentences: [
                { text: "Ông ngoại của bé.", icons: ["👴", "👨‍🦳", "👴"] },
                { text: "Cái võng của ông.", icons: ["🪢", "👴", "🌳"] },
                { text: "Bé bồng gấu bông.", icons: ["👧", "🧸", "🤗"] },
                { text: "Cồng kềnh, cồng kềnh.", icons: ["📦", "📦", "📦"] },
                { text: "Ông giáo làng.", icons: ["👨‍🏫", "🏫", "👨‍🦳"] },
                { text: "Gió lộng trên sông.", icons: ["🌬️", "🌊", "💨"] },
                { text: "Ông nội của bé.", icons: ["👴", "👨‍🦳", "👴"] },
                { text: "Ông bà rất tốt.", icons: ["👴", "👵", "💖"] },
                { text: "Ông ngoại.", icons: ["👴", "👨‍🦳", "👴"] },
                { text: "Cái võng.", icons: ["🪢", "😴", "😌"] },
                { text: "Bé bồng.", icons: ["👧", "👶", "🤱"] },
                { text: "Cồng kềnh.", icons: ["📦", "📦", "📦"] },
                { text: "Ông giáo.", icons: ["👨‍🏫", "🏫", "👨‍🦳"] },
                { text: "Gió lộng.", icons: ["🌬️", "💨", "🌊"] },
                { text: "Ông nội.", icons: ["👴", "👨‍🦳", "👴"] },
                { text: "Ông bà.", icons: ["👴", "👵", "💖"] },
                { text: "Ông mặt trời.", icons: ["☀️", "🌞", "🌅"] },
                { text: "Ông tiên.", icons: ["🧚‍♀️", "✨", "👑"] },
                { text: "Ông già.", icons: ["👴", "👨‍🦳", "🧓"] },
                { text: "Ông chủ.", icons: ["🧑‍💼", "👨‍💼", "👔"] }
            ]},
            { id: "EM", label: "EM", title: "Bé Học Vần EM", themeClass: "theme-em", sentences: [
                { text: "Con tem của ba.", icons: ["✉️", "👨", "📮"] },
                { text: "Bé xem tivi.", icons: ["👧", "📺", "👀"] },
                { text: "Cái xem của em.", icons: ["🚲", "👧", "👦"] },
                { text: "Bé kem rất thích ăn.", icons: ["👧", "🍦", "😋"] },
                { text: "Em bé của mẹ.", icons: ["👶", "👩", "💖"] },
                { text: "Đèn đường buổi đêm.", icons: ["💡", "🌃", "✨"] },
                { text: "Em thích ca hát.", icons: ["🎶", "🎤", "😊"] },
                { text: "Cái kem ngon quá.", icons: ["🍦", "🤤", "😋"] },
                { text: "Em em, em em.", icons: ["👶", "👧", "👦"] },
                { text: "Em ăn kem.", icons: ["👧", "🍦", "😋"] },
                { text: "Con tem.", icons: ["✉️", " stamp", "📜"] },
                { text: "Xem tivi.", icons: ["📺", "👀", "👀"] },
                { text: "Cái xem.", icons: ["🚲", "🛵", "🏍️"] },
                { text: "Kem.", icons: ["🍦", "🍦", "🍦"] },
                { text: "Em bé.", icons: ["👶", "👶", "👶"] },
                { text: "Đêm.", icons: ["🌃", "🌌", "🌙"] },
                { text: "Em.", icons: ["👧", "👦", "🧒"] },
                { text: "Xem.", icons: ["👀", "👀", "👀"] },
                { text: "Kem.", icons: ["🍦", "🍦", "🍦"] },
                { text: "Em bé.", icons: ["👶", "👶", "👶"] }
            ]},
            { id: "ÊM", label: "ÊM", title: "Bé Học Vần ÊM", themeClass: "theme-em-hat", sentences: [
                { text: "Êm êm tiếng gió thổi.", icons: ["🌬️", "🍃", "🌬️"] },
                { text: "Bé nằm êm trên giường.", icons: ["👧", "🛌", "😌"] },
                { text: "Mềm êm như mây.", icons: ["☁️", "💖", "😊"] },
                { text: "Cái gối rất êm.", icons: ["🛏️", "😌", "😴"] },
                { text: "Lên lớp thật êm.", icons: ["🏫", "🤫", "🚶"] },
                { text: "Êm đềm buổi chiều.", icons: ["🌆", "😌", "😊"] },
                { text: "Êm êm, êm êm.", icons: ["🎶", "🎵", "🔊"] },
                { text: "Bé nằm êm.", icons: ["👧", "😴", "😌"] },
                { text: "Êm ái.", icons: ["💖", "😌", "😊"] },
                { text: "Êm đềm.", icons: ["😊", "😌", "💖"] },
                { text: "Cái gối êm.", icons: ["🛏️", "😌", "😴"] },
                { text: "Êm ái.", icons: ["💖", "😌", "😊"] },
                { text: "Êm đềm.", icons: ["😊", "😌", "💖"] },
                { text: "Êm êm.", icons: ["🎶", "🎵", "🔊"] },
                { text: "Cái gối.", icons: ["🛏️", "😴", "😌"] },
                { text: "Êm ái.", icons: ["💖", "😌", "😊"] },
                { text: "Êm đềm.", icons: ["😊", "😌", "💖"] },
                { text: "Êm êm.", icons: ["🎶", "🎵", "🔊"] },
                { text: "Cái gối.", icons: ["🛏️", "😴", "😌"] },
                { text: "Êm ái.", icons: ["💖", "😌", "😊"] }
            ]},
            { id: "IM", label: "IM", title: "Bé Học Vần IM", themeClass: "theme-im", sentences: [
                { text: "Con chim bay.", icons: ["🐦", "🌬️", "☁️"] },
                { text: "Cái kim may áo.", icons: ["🪡", "🧵", "👚"] },
                { text: "Im lặng, im lặng.", icons: ["🤫", "🤫", "🤫"] },
                { text: "Kim chỉ của bà.", icons: ["🪡", "🧵", "👵"] },
                { text: "Bé thích xem phim.", icons: ["👧", "🎬", "🍿"] },
                { text: "Màu tím của hoa.", icons: ["💜", "🌸", "💖"] },
                { text: "Chim bay trên trời.", icons: ["🐦", "☁️", "⬆️"] },
                { text: "Im lặng để nghe.", icons: ["🤫", "👂", "😊"] },
                { text: "Cái kim khâu.", icons: ["🪡", "🧵", "🧶"] },
                { text: "Chim hót.", icons: ["🐦", "🎶", "🎤"] },
                { text: "Con chim.", icons: ["🐦", "🐦", "🐦"] },
                { text: "Cái kim.", icons: ["🪡", "🪡", "🪡"] },
                { text: "Im lặng.", icons: ["🤫", "🤫", "🤫"] },
                { text: "Phim.", icons: ["🎬", "🍿", "🎥"] },
                { text: "Màu tím.", icons: ["💜", "💜", "💜"] },
                { text: "Chim bay.", icons: ["🐦", "🌬️", "☁️"] },
                { text: "Im.", icons: ["🤫", "🤫", "🤫"] },
                { text: "Kim.", icons: ["🪡", "🪡", "🪡"] },
                { text: "Im.", icons: ["🤫", "🤫", "🤫"] },
                { text: "Chim.", icons: ["🐦", "🐦", "🐦"] }
            ]},
            { id: "UM", label: "UM", title: "Bé Học Vần UM", themeClass: "theme-um", sentences: [
                { text: "Bé ngủ trong đêm.", icons: ["👧", "😴", "🌃"] },
                { text: "Cái chùm bóng bay.", icons: ["🎈", "🎈", "🎈"] },
                { text: "Bé mỉm cười.", icons: ["😊", "😂", "💖"] },
                { text: "Cái chum nước.", icons: ["🏺", "💧", "🌊"] },
                { text: "Bé đi vào đêm.", icons: ["👦", "🌃", "🚶"] },
                { text: "Bạn làm thùm.", icons: ["🤸", "💥", "🔊"] },
                { text: "Cái chùm quả.", icons: ["🍇", "🍇", "🍇"] },
                { text: "Bé ngủ muộn.", icons: ["👧", "😴", "⏰"] },
                { text: "Chùm chìa khóa.", icons: ["🔑", "🔑", "🔑"] },
                { text: "Bé đi vào đêm.", icons: ["👦", "🌃", "🚶"] },
                { text: "Chùm bóng.", icons: ["🎈", "🎈", "🎈"] },
                { text: "Cái chum.", icons: ["🏺", "💧", "🌊"] },
                { text: "Chùm quả.", icons: ["🍇", "🍇", "🍇"] },
                { text: "Bé ngủ đêm.", icons: ["👧", "😴", "🌃"] },
                { text: "Thùm.", icons: ["💥", "🔊", "💥"] },
                { text: "Đêm.", icons: ["🌃", "🌌", "🌙"] },
                { text: "Chum.", icons: ["🏺", "💧", "🌊"] },
                { text: "Chùm.", icons: ["🍇", "🍇", "🍇"] },
                { text: "Đêm.", icons: ["🌃", "🌌", "🌙"] },
                { text: "Bé mỉm cười.", icons: ["😊", "😂", "💖"] }
            ]},
            { id: "IN", label: "IN", title: "Bé Học Vần IN", themeClass: "theme-in", sentences: [
                { text: "Cái đinh đóng gỗ.", icons: ["🔨", "🪵", "🔩"] },
                { text: "Bé xin phép bố mẹ.", icons: ["👧", "🙏", "👨‍👩‍👧‍👦"] },
                { text: "Cái in của ba.", icons: ["🖨️", "👨", "📄"] },
                { text: "Bé rất xinh xắn.", icons: ["👧", "💖", "✨"] },
                { text: "Tin tôi đi.", icons: ["👍", "🤝", "😊"] },
                { text: "Bé ăn xin.", icons: ["👧", "🙏", "😋"] },
                { text: "Tin nhắn của mẹ.", icons: ["✉️", "👩", "💬"] },
                { text: "In ra giấy.", icons: ["🖨️", "📄", "✍️"] },
                { text: "Bé xin kẹo.", icons: ["👧", "🍬", "🍭"] },
                { text: "Cái đinh.", icons: ["🔨", "🔩", "🔩"] },
                { text: "Bé xin phép.", icons: ["👧", "🙏", "😊"] },
                { text: "Cái in.", icons: ["🖨️", "📄", "✍️"] },
                { text: "Bé xinh.", icons: ["👧", "💖", "✨"] },
                { text: "Tin.", icons: ["👍", "🤝", "😊"] },
                { text: "Bé ăn xin.", icons: ["👧", "🙏", "😋"] },
                { text: "Tin nhắn.", icons: ["✉️", "💬", "✉️"] },
                { text: "In.", icons: ["🖨️", "📄", "✍️"] },
                { text: "Bé xin.", icons: ["👧", "🙏", "😊"] },
                { text: "Cái đinh.", icons: ["🔨", "🔩", "🔩"] },
                { text: "Tin.", icons: ["👍", "🤝", "😊"] }
            ]},
            { id: "UN", label: "UN", title: "Bé Học Vần UN", themeClass: "theme-un", sentences: [
                { text: "Bé buồn quá.", icons: ["👧", "😔", "😞"] },
                { text: "Bé không buồn.", icons: ["👧", "😊", "💖"] },
                { text: "Chun chun, chun chun.", icons: ["🎶", "🎵", "🔊"] },
                { text: "Bé rất buồn.", icons: ["👦", "😔", "😞"] },
                { text: "Buồn bã, buồn rầu.", icons: ["😔", "😞", "😭"] },
                { text: "Bé không buồn.", icons: ["👧", "😊", "💖"] },
                { text: "Buồn ngủ rồi.", icons: ["😴", "😌", "😴"] },
                { text: "Bé buồn.", icons: ["👧", "😔", "😞"] },
                { text: "Buồn.", icons: ["😔", "😞", "😭"] },
                { text: "Buồn.", icons: ["😔", "😞", "😭"] },
                { text: "Bé buồn ngủ.", icons: ["👧", "😴", "😌"] },
                { text: "Buồn.", icons: ["😔", "😞", "😭"] },
                { text: "Bé không buồn.", icons: ["👧", "😊", "💖"] },
                { text: "Buồn.", icons: ["😔", "😞", "😭"] },
                { text: "Buồn.", icons: ["😔", "😞", "😭"] },
                { text: "Buồn ngủ.", icons: ["😴", "😌", "😴"] },
                { text: "Bé buồn.", icons: ["👧", "😔", "😞"] },
                { text: "Buồn.", icons: ["😔", "😞", "😭"] },
                { text: "Buồn.", icons: ["😔", "😞", "😭"] },
                { text: "Buồn ngủ.", icons: ["😴", "😌", "😴"] }
            ]},
            { id: "ÔM", label: "ÔM", title: "Bé Học Vần ÔM", themeClass: "theme-om-hat", sentences: [
                { text: "Bé ôm gấu bông.", icons: ["👧", "🧸", "🤗"] },
                { text: "Bé ôm mẹ thật chặt.", icons: ["👧", "👩", "🤗"] },
                { text: "Bé ôm ba.", icons: ["👧", "👨", "🤗"] },
                { text: "Bé ôm em.", icons: ["👧", "👶", "🤗"] },
                { text: "Bé ôm bạn.", icons: ["👧", "👦", "🤗"] },
                { text: "Ôm cây.", icons: ["🌳", "🤗", "🌳"] },
                { text: "Ôm lấy mẹ.", icons: ["👩", "🤗", "💖"] },
                { text: "Ôm con.", icons: ["👩", "👶", "🤗"] },
                { text: "Ôm lấy em.", icons: ["👧", "👶", "🤗"] },
                { text: "Ôm bạn.", icons: ["👧", "👦", "🤗"] },
                { text: "Bé ôm ba.", icons: ["👧", "👨", "🤗"] },
                { text: "Ôm.", icons: ["🤗", "🤗", "🤗"] },
                { text: "Ôm mẹ.", icons: ["👩", "🤗", "💖"] },
                { text: "Ôm.", icons: ["🤗", "🤗", "🤗"] },
                { text: "Ôm.", icons: ["🤗", "🤗", "🤗"] },
                { text: "Ôm.", icons: ["🤗", "🤗", "🤗"] },
                { text: "Ôm.", icons: ["🤗", "🤗", "🤗"] },
                { text: "Ôm.", icons: ["🤗", "🤗", "🤗"] },
                { text: "Ôm.", icons: ["🤗", "🤗", "🤗"] },
                { text: "Ôm.", icons: ["🤗", "🤗", "🤗"] }
            ]},
            { id: "ƠM", label: "ƠM", title: "Bé Học Vần ƠM", themeClass: "theme-om-mo", sentences: [
                { text: "Bé lượm đồ chơi.", icons: ["👧", "🧸", "🚶"] },
                { text: "Bé lượm rác.", icons: ["👧", "♻️", "🗑️"] },
                { text: "Bạn Lượm rất tốt.", icons: ["👦", "👍", "💖"] },
                { text: "Lượm lặt, lượm lặt.", icons: ["🚶", "🚶", "🔍"] },
                { text: "Bé lượm kẹo.", icons: ["👧", "🍬", "🍭"] },
                { text: "Lượm hạt.", icons: ["🫘", "🚶", "🔍"] },
                { text: "Lượm rác.", icons: ["♻️", "🗑️", "👍"] },
                { text: "Bé Lượm.", icons: ["👦", "👧", "🧑"] },
                { text: "Lượm.", icons: ["🚶", "🔍", "🚶"] },
                { text: "Lượm.", icons: ["🚶", "🔍", "🚶"] },
                { text: "Bé lượm kẹo.", icons: ["👧", "🍬", "🍭"] },
                { text: "Lượm.", icons: ["🚶", "🔍", "🚶"] },
                { text: "Lượm.", icons: ["🚶", "🔍", "🚶"] },
                { text: "Lượm.", icons: ["🚶", "🔍", "🚶"] },
                { text: "Bé lượm kẹo.", icons: ["👧", "🍬", "🍭"] },
                { text: "Lượm.", icons: ["🚶", "🔍", "🚶"] },
                { text: "Lượm.", icons: ["🚶", "🔍", "🚶"] },
                { text: "Lượm.", icons: ["🚶", "🔍", "🚶"] },
                { text: "Bé lượm kẹo.", icons: ["👧", "🍬", "🍭"] },
                { text: "Lượm.", icons: ["🚶", "🔍", "🚶"] }
            ]},
            { id: "IU", label: "IU", title: "Bé Học Vần IU", themeClass: "theme-iu", sentences: [
                { text: "Tiu nghỉu, tiu nghỉu.", icons: ["😔", "😞", "😭"] },
                { text: "Bé xiu xiu.", icons: ["👧", "😔", "😞"] },
                { text: "Con tiu béo.", icons: ["🐷", "🐖", "🐽"] },
                { text: "Bé chịu thua.", icons: ["👧", "👎", "😠"] },
                { text: "Con tiu đi đâu.", icons: ["🐷", "🏃", "💨"] },
                { text: "Bé xiu xiu rồi.", icons: ["👧", "😔", "😞"] },
                { text: "Bé chịu thua.", icons: ["👧", "👎", "😠"] },
                { text: "Con tiu.", icons: ["🐷", "🐖", "🐽"] },
                { text: "Bé xiu xiu.", icons: ["👧", "😔", "😞"] },
                { text: "Bé chịu thua.", icons: ["👧", "👎", "😠"] },
                { text: "Con tiu.", icons: ["🐷", "🐖", "🐽"] },
                { text: "Bé xiu xiu.", icons: ["👧", "😔", "😞"] },
                { text: "Bé chịu thua.", icons: ["👧", "👎", "😠"] },
                { text: "Con tiu.", icons: ["🐷", "🐖", "🐽"] },
                { text: "Bé xiu xiu.", icons: ["👧", "😔", "😞"] },
                { text: "Bé chịu thua.", icons: ["👧", "👎", "😠"] },
                { text: "Con tiu.", icons: ["🐷", "🐖", "🐽"] },
                { text: "Bé xiu xiu.", icons: ["👧", "😔", "😞"] },
                { text: "Bé chịu thua.", icons: ["👧", "👎", "😠"] },
                { text: "Con tiu.", icons: ["🐷", "🐖", "🐽"] }
            ]},
            { id: "ÊU", label: "ÊU", title: "Bé Học Vần ÊU", themeClass: "theme-eu", sentences: [
                { text: "Bé kêu cứu.", icons: ["👧", "📢", "🗣️"] },
                { text: "Bé kêu meo meo.", icons: ["👧", "😺", "🔊"] },
                { text: "Con trâu kéo cày.", icons: ["🐂", "🚜", "🌾"] },
                { text: "Bạn êu cầu giúp đỡ.", icons: ["👦", "🤝", "🙏"] },
                { text: "Bé kêu to.", icons: ["👧", "📢", "🗣️"] },
                { text: "Con trâu.", icons: ["🐂", "🐄", "🐮"] },
                { text: "Bé kêu.", icons: ["👧", "📢", "🗣️"] },
                { text: "Bạn êu.", icons: ["👦", "👧", "🧑"] },
                { text: "Con trâu.", icons: ["🐂", "🐄", "🐮"] },
                { text: "Bé kêu.", icons: ["👧", "📢", "🗣️"] },
                { text: "Bạn êu.", icons: ["👦", "👧", "🧑"] },
                { text: "Con trâu.", icons: ["🐂", "🐄", "🐮"] },
                { text: "Bé kêu.", icons: ["👧", "📢", "🗣️"] },
                { text: "Bạn êu.", icons: ["👦", "👧", "🧑"] },
                { text: "Con trâu.", icons: ["🐂", "🐄", "🐮"] },
                { text: "Bé kêu.", icons: ["👧", "📢", "🗣️"] },
                { text: "Bạn êu.", icons: ["👦", "👧", "🧑"] },
                { text: "Con trâu.", icons: ["🐂", "🐄", "🐮"] },
                { text: "Bé kêu.", icons: ["👧", "📢", "🗣️"] },
                { text: "Bạn êu.", icons: ["👦", "👧", "🧑"] }
            ]},
            { id: "UI", label: "UI", title: "Bé Học Vần UI", themeClass: "theme-ui", sentences: [
                { text: "Bé vui vẻ đi chơi.", icons: ["👧", "😊", "🤸"] },
                { text: "Cái túi của mẹ.", icons: ["👜", "👩", "🛍️"] },
                { text: "Con múi bay.", icons: [" mosquito", "💨", "🌬️"] },
                { text: "Bé mui vào chăn.", icons: ["👧", "🛌", "😴"] },
                { text: "Bé vui vẻ.", icons: ["👦", "😊", "😂"] },
                { text: "Cái túi của ba.", icons: ["💼", "👨", "💼"] },
                { text: "Con múi.", icons: [" mosquito", "💨", "🌬️"] },
                { text: "Bé mui.", icons: ["👧", "🛌", "😴"] },
                { text: "Bé vui vẻ.", icons: ["👦", "😊", "😂"] },
                { text: "Cái túi.", icons: ["👜", "🛍️", "💼"] },
                { text: "Vui vẻ.", icons: ["😊", "😂", "💖"] },
                { text: "Túi.", icons: ["👜", "🛍️", "💼"] },
                { text: "Con múi.", icons: [" mosquito", "💨", "🌬️"] },
                { text: "Mui.", icons: ["🛌", "😴", "😌"] },
                { text: "Vui vẻ.", icons: ["😊", "😂", "💖"] },
                { text: "Túi.", icons: ["👜", "🛍️", "💼"] },
                { text: "Con múi.", icons: [" mosquito", "💨", "🌬️"] },
                { text: "Mui.", icons: ["🛌", "😴", "😌"] },
                { text: "Vui vẻ.", icons: ["😊", "😂", "💖"] },
                { text: "Túi.", icons: ["👜", "🛍️", "💼"] }
            ]},
            { id: "ƯI", label: "ƯI", title: "Bé Học Vần ƯI", themeClass: "theme-ui-mo", sentences: [
                { text: "Cái lưỡi của bạn.", icons: ["👅", "👦", "👧"] },
                { text: "Bạn cười thật vui.", icons: ["😂", "😊", "💖"] },
                { text: "Bé lười biếng.", icons: ["👧", "😴", "😖"] },
                { text: "Bé cười.", icons: ["👦", "😂", "😊"] },
                { text: "Cái lưỡi.", icons: ["👅", " tongue", "👄"] },
                { text: "Lười biếng.", icons: ["😴", "😖", "😴"] },
                { text: "Cười.", icons: ["😂", "😊", "💖"] },
                { text: "Cái lưỡi.", icons: ["👅", " tongue", "👄"] },
                { text: "Lười biếng.", icons: ["😴", "😖", "😴"] },
                { text: "Cười.", icons: ["😂", "😊", "💖"] },
                { text: "Cái lưỡi.", icons: ["👅", " tongue", "👄"] },
                { text: "Lười biếng.", icons: ["😴", "😖", "😴"] },
                { text: "Cười.", icons: ["😂", "😊", "💖"] },
                { text: "Cái lưỡi.", icons: ["👅", " tongue", "👄"] },
                { text: "Lười biếng.", icons: ["😴", "😖", "😴"] },
                { text: "Cười.", icons: ["😂", "😊", "💖"] },
                { text: "Cái lưỡi.", icons: ["👅", " tongue", "👄"] },
                { text: "Lười biếng.", icons: ["😴", "😖", "😴"] },
                { text: "Cười.", icons: ["😂", "😊", "💖"] },
                { text: "Cái lưỡi.", icons: ["👅", " tongue", "👄"] }
            ]},
            { id: "OT", label: "OT", title: "Bé Học Vần OT", themeClass: "theme-ot", sentences: [
                { text: "Con thỏ rất thích cà rốt.", icons: ["🐇", "🥕", "😋"] },
                { text: "Cái bọt xà phòng.", icons: ["🫧", "🧼", "✨"] },
                { text: "Bé hót hòn hén.", icons: ["👦", "😭", "💧"] },
                { text: "Con chót bay.", icons: ["🐦", "🌬️", "☁️"] },
                { text: "Cái chót to.", icons: ["🐦", "😮", "💖"] },
                { text: "Bọt xà phòng.", icons: ["🫧", "🧼", "✨"] },
                { text: "Hót hòn hén.", icons: ["😭", "💧", "😭"] },
                { text: "Chót.", icons: ["🐦", "🐦", "🐦"] },
                { text: "Hót hòn hén.", icons: ["😭", "💧", "😭"] },
                { text: "Chót.", icons: ["🐦", "🐦", "🐦"] },
                { text: "Bọt.", icons: ["🫧", "🧼", "✨"] },
                { text: "Hót.", icons: ["😭", "💧", "😭"] },
                { text: "Chót.", icons: ["🐦", "🐦", "🐦"] },
                { text: "Bọt.", icons: ["🫧", "🧼", "✨"] },
                { text: "Hót.", icons: ["😭", "💧", "😭"] },
                { text: "Chót.", icons: ["🐦", "🐦", "🐦"] },
                { text: "Bọt.", icons: ["🫧", "🧼", "✨"] },
                { text: "Hót.", icons: ["😭", "💧", "😭"] },
                { text: "Chót.", icons: ["🐦", "🐦", "🐦"] },
                { text: "Bọt.", icons: ["🫧", "🧼", "✨"] }
            ]},
            { id: "AT", label: "AT", title: "Bé Học Vần AT", themeClass: "theme-at", sentences: [
                { text: "Con mèo rất bát nháo.", icons: ["😺", "😠", "😤"] },
                { text: "Bé chạy thoát ra.", icons: ["👦", "🏃", "💨"] },
                { text: "Cái giật mình.", icons: ["😮", " startled", "👀"] },
                { text: "Bé rất nhát gan.", icons: ["👧", "🫣", "😨"] },
                { text: "Bát cơm của bé.", icons: ["🥣", "🍚", "😋"] },
                { text: "Cái giật mình.", icons: ["😮", " startled", "👀"] },
                { text: "Bé nhát gan.", icons: ["👧", "🫣", "😨"] },
                { text: "Bát cơm.", icons: ["🥣", "🍚", "😋"] },
                { text: "Giật mình.", icons: ["😮", " startled", "👀"] },
                { text: "Nhát gan.", icons: ["🫣", "😨", "😖"] },
                { text: "Bát.", icons: ["🥣", "🍚", "😋"] },
                { text: "Giật.", icons: ["😮", " startled", "👀"] },
                { text: "Nhát.", icons: ["🫣", "😨", "😖"] },
                { text: "Bát.", icons: ["🥣", "🍚", "😋"] },
                { text: "Giật.", icons: ["😮", " startled", "👀"] },
                { text: "Nhát.", icons: ["🫣", "😨", "😖"] },
                { text: "Bát.", icons: ["🥣", "🍚", "😋"] },
                { text: "Giật.", icons: ["😮", " startled", "👀"] },
                { text: "Nhát.", icons: ["🫣", "😨", "😖"] },
                { text: "Bát.", icons: ["🥣", "🍚", "😋"] }
            ]},
            { id: "ET", label: "ET", title: "Bé Học Vần ET", themeClass: "theme-et", sentences: [
                { text: "Bé rất mệt mỏi.", icons: ["👧", "😴", "😔"] },
                { text: "Cái két sắt.", icons: ["🔒", "💰", "💎"] },
                { text: "Bé hét lên.", icons: ["👦", "📢", "🗣️"] },
                { text: "Mệt rồi thì nghỉ.", icons: ["😴", "🛌", "😌"] },
                { text: "Cái két to.", icons: ["🔒", "😮", "💖"] },
                { text: "Bé hét.", icons: ["👦", "📢", "🗣️"] },
                { text: "Mệt.", icons: ["😴", "😔", "😖"] },
                { text: "Két.", icons: ["🔒", "💰", "💎"] },
                { text: "Hét.", icons: ["📢", "🗣️", "📢"] },
                { text: "Mệt.", icons: ["😴", "😔", "😖"] },
                { text: "Két.", icons: ["🔒", "💰", "💎"] },
                { text: "Hét.", icons: ["📢", "🗣️", "📢"] },
                { text: "Mệt.", icons: ["😴", "😔", "😖"] },
                { text: "Két.", icons: ["🔒", "💰", "💎"] },
                { text: "Hét.", icons: ["📢", "🗣️", "📢"] },
                { text: "Mệt.", icons: ["😴", "😔", "😖"] },
                { text: "Két.", icons: ["🔒", "💰", "💎"] },
                { text: "Hét.", icons: ["📢", "🗣️", "📢"] },
                { text: "Mệt.", icons: ["😴", "😔", "😖"] },
                { text: "Két.", icons: ["🔒", "💰", "💎"] }
            ]},
            { id: "ÊT", label: "ÊT", title: "Bé Học Vần ÊT", themeClass: "theme-et-hat", sentences: [
                { text: "Bé hệt như mẹ.", icons: ["👧", "👩", "💖"] },
                { text: "Rất ghét món này.", icons: ["😠", "😤", "👎"] },
                { text: "Bé có một vết thương.", icons: ["👧", "🩹", "🤕"] },
                { text: "Ghét cái nóng.", icons: ["😠", "🥵", "☀️"] },
                { text: "Vết thương nhỏ.", icons: ["🩹", "🤏", "🤕"] },
                { text: "Ghét cái lạnh.", icons: ["😠", "🥶", "🧣"] },
                { text: "Bé hệt như ba.", icons: ["👦", "👨", "👍"] },
                { text: "Ghét.", icons: ["😠", "😤", "👎"] },
                { text: "Vết.", icons: ["🩹", "🤕", "🩹"] },
                { text: "Ghét.", icons: ["😠", "😤", "👎"] },
                { text: "Vết.", icons: ["🩹", "🤕", "🩹"] },
                { text: "Ghét.", icons: ["😠", "😤", "👎"] },
                { text: "Vết.", icons: ["🩹", "🤕", "🩹"] },
                { text: "Ghét.", icons: ["😠", "😤", "👎"] },
                { text: "Vết.", icons: ["🩹", "🤕", "🩹"] },
                { text: "Ghét.", icons: ["😠", "😤", "👎"] },
                { text: "Vết.", icons: ["🩹", "🤕", "🩹"] },
                { text: "Ghét.", icons: ["😠", "😤", "👎"] },
                { text: "Vết.", icons: ["🩹", "🤕", "🩹"] },
                { text: "Ghét.", icons: ["😠", "😤", "👎"] }
            ]},
            { id: "IT", label: "IT", title: "Bé Học Vần IT", themeClass: "theme-it", sentences: [
                { text: "Mẹ mua một ít kẹo.", icons: ["👩", "🛍️", "🍬"] },
                { text: "Con vịt kêu quít quít.", icons: ["🦆", "🔊", "🎶"] },
                { text: "Bé hít vào thật sâu.", icons: ["👃", "🌬️", "😌"] },
                { text: "Một ít thôi.", icons: ["🤏", "🤏", "🤏"] },
                { text: "Bé hít vào.", icons: ["👃", "🌬️", "😌"] },
                { text: "Một ít.", icons: ["🤏", "🤏", "🤏"] },
                { text: "Hít.", icons: ["👃", "🌬️", "😌"] },
                { text: "Ít.", icons: ["🤏", "🤏", "🤏"] },
                { text: "Hít.", icons: ["👃", "🌬️", "😌"] },
                { text: "Ít.", icons: ["🤏", "🤏", "🤏"] },
                { text: "Hít.", icons: ["👃", "🌬️", "😌"] },
                { text: "Ít.", icons: ["🤏", "🤏", "🤏"] },
                { text: "Hít.", icons: ["👃", "🌬️", "😌"] },
                { text: "Ít.", icons: ["🤏", "🤏", "🤏"] },
                { text: "Hít.", icons: ["👃", "🌬️", "😌"] },
                { text: "Ít.", icons: ["🤏", "🤏", "🤏"] },
                { text: "Hít.", icons: ["👃", "🌬️", "😌"] },
                { text: "Ít.", icons: ["🤏", "🤏", "🤏"] },
                { text: "Hít.", icons: ["👃", "🌬️", "😌"] },
                { text: "Ít.", icons: ["🤏", "🤏", "🤏"] }
            ]},
            { id: "IA", label: "IA", title: "Bé Học Vần IA", themeClass: "theme-ia", sentences: [
                { text: "Con đĩa bám vào tay.", icons: ["🪱", "✋", "🤢"] },
                { text: "Bé kia đang làm gì?", icons: ["👦", "❓", "🤔"] },
                { text: "Cả nhà cùng chia nhau.", icons: ["👨‍👩‍👧‍👦", " 나눠", "😊"] },
                { text: "Bé đi chơi với bạn Nia.", icons: ["👧", "👦", "🤸"] },
                { text: "Bé chia kẹo.", icons: ["👧", "🍬", "🍭"] },
                { text: "Chia sẻ.", icons: ["🤝", "💖", "😊"] },
                { text: "Con đĩa.", icons: ["🪱", "🪱", "🪱"] },
                { text: "Kia.", icons: ["👉", "👉", "👉"] },
                { text: "Chia.", icons: [" 나눠", " 나눠", " 나눠"] },
                { text: "Bé đi.", icons: ["👧", "🚶", "🚶"] },
                { text: "Bé chia.", icons: ["👧", " 나눠", " 나눠"] },
                { text: "Chia sẻ.", icons: ["🤝", "💖", "😊"] },
                { text: "Con đĩa.", icons: ["🪱", "🪱", "🪱"] },
                { text: "Kia.", icons: ["👉", "👉", "👉"] },
                { text: "Chia.", icons: [" 나눠", " 나눠", " 나눠"] },
                { text: "Bé đi.", icons: ["👧", "🚶", "🚶"] },
                { text: "Bé chia.", icons: ["👧", " 나눠", " 나눠"] },
                { text: "Chia sẻ.", icons: ["🤝", "💖", "😊"] },
                { text: "Con đĩa.", icons: ["🪱", "🪱", "🪱"] },
                { text: "Kia.", icons: ["👉", "👉", "👉"] }
            ]},
            { id: "UÔI", label: "UÔI", title: "Bé Học Vần UÔI", themeClass: "theme-uoi", sentences: [
                { text: "Đuôi con chó.", icons: ["🐶", "🐕", "🐾"] },
                { text: "Cái muỗng của bé.", icons: ["🥄", "👦", "👧"] },
                { text: "Bé đuổi theo bạn.", icons: ["👦", "🏃", "💨"] },
                { text: "Con suối chảy.", icons: ["💧", "🌊", "🏞️"] },
                { text: "Cái đuôi.", icons: ["🐶", "🐕", "🐾"] },
                { text: "Cái muỗng.", icons: ["🥄", "🥄", "🥄"] },
                { text: "Đuổi.", icons: ["🏃", "💨", "💨"] },
                { text: "Suối.", icons: ["💧", "🌊", "🏞️"] },
                { text: "Đuôi.", icons: ["🐶", "🐕", "🐾"] },
                { text: "Muỗng.", icons: ["🥄", "🥄", "🥄"] },
                { text: "Đuổi.", icons: ["🏃", "💨", "💨"] },
                { text: "Suối.", icons: ["💧", "🌊", "🏞️"] },
                { text: "Đuôi.", icons: ["🐶", "🐕", "🐾"] },
                { text: "Muỗng.", icons: ["🥄", "🥄", "🥄"] },
                { text: "Đuổi.", icons: ["🏃", "💨", "💨"] },
                { text: "Suối.", icons: ["💧", "🌊", "🏞️"] },
                { text: "Đuôi.", icons: ["🐶", "🐕", "🐾"] },
                { text: "Muỗng.", icons: ["🥄", "🥄", "🥄"] },
                { text: "Đuổi.", icons: ["🏃", "💨", "💨"] },
                { text: "Suối.", icons: ["💧", "🌊", "🏞️"] }
            ]},
            { id: "ANH", label: "ANH", title: "Bé Học Vần ANH", themeClass: "theme-anh", sentences: [
                { text: "Anh trai của bé.", icons: ["👦", "👨‍🦱", "👍"] },
                { text: "Bé đi học rất nhanh.", icons: ["👧", "🏃", "💨"] },
                { text: "Anh trai của con.", icons: ["👦", "👨‍🦱", "👍"] },
                { text: "Bé nhanh nhẹn.", icons: ["👧", "🤸", "💪"] },
                { text: "Anh trai của bé.", icons: ["👦", "👨‍🦱", "👍"] },
                { text: "Nhanh lên.", icons: ["🏃", "💨", "💨"] },
                { text: "Anh.", icons: ["👦", "👨‍🦱", "👍"] },
                { text: "Nhanh.", icons: ["🏃", "💨", "💨"] },
                { text: "Anh.", icons: ["👦", "👨‍🦱", "👍"] },
                { text: "Nhanh.", icons: ["🏃", "💨", "💨"] },
                { text: "Anh.", icons: ["👦", "👨‍🦱", "👍"] },
                { text: "Nhanh.", icons: ["🏃", "💨", "💨"] },
                { text: "Anh.", icons: ["👦", "👨‍🦱", "👍"] },
                { text: "Nhanh.", icons: ["🏃", "💨", "💨"] },
                { text: "Anh.", icons: ["👦", "👨‍🦱", "👍"] },
                { text: "Nhanh.", icons: ["🏃", "💨", "💨"] },
                { text: "Anh.", icons: ["👦", "👨‍🦱", "👍"] },
                { text: "Nhanh.", icons: ["🏃", "💨", "💨"] },
                { text: "Anh.", icons: ["👦", "👨‍🦱", "👍"] },
                { text: "Nhanh.", icons: ["🏃", "💨", "💨"] }
            ]},
            { id: "ACH", label: "ACH", title: "Bé Học Vần ACH", themeClass: "theme-ach", sentences: [
                { text: "Bé lạch bạch.", icons: ["👧", "🚶", "🚶"] },
                { text: "Đạt giải nhất.", icons: ["🏆", "🥇", "✨"] },
                { text: "Bé lạch bạch.", icons: ["👦", "🚶", "🚶"] },
                { text: "Đạt giải.", icons: ["🏆", "🥇", "✨"] },
                { text: "Bé lạch bạch.", icons: ["👧", "🚶", "🚶"] },
                { text: "Đạt giải.", icons: ["🏆", "🥇", "✨"] },
                { text: "Bé lạch bạch.", icons: ["👦", "🚶", "🚶"] },
                { text: "Đạt giải.", icons: ["🏆", "🥇", "✨"] },
                { text: "Bé lạch bạch.", icons: ["👧", "🚶", "🚶"] },
                { text: "Đạt giải.", icons: ["🏆", "🥇", "✨"] },
                { text: "Bé lạch bạch.", icons: ["👦", "🚶", "🚶"] },
                { text: "Đạt giải.", icons: ["🏆", "🥇", "✨"] },
                { text: "Bé lạch bạch.", icons: ["👧", "🚶", "🚶"] },
                { text: "Đạt giải.", icons: ["🏆", "🥇", "✨"] },
                { text: "Bé lạch bạch.", icons: ["👦", "🚶", "🚶"] },
                { text: "Đạt giải.", icons: ["🏆", "🥇", "✨"] },
                { text: "Bé lạch bạch.", icons: ["👧", "🚶", "🚶"] },
                { text: "Đạt giải.", icons: ["🏆", "🥇", "✨"] },
                { text: "Bé lạch bạch.", icons: ["👦", "🚶", "🚶"] },
                { text: "Đạt giải.", icons: ["🏆", "🥇", "✨"] }
            ]},
            { id: "IÊN", label: "IÊN", title: "Bé Học Vần IÊN", themeClass: "theme-ien", sentences: [
                { text: "Chiếc thuyền trôi.", icons: ["⛵", "🌊", "💨"] },
                { text: "Tiếng chim hót.", icons: ["🐦", "🎶", "🎤"] },
                { text: "Yên lặng lắng nghe.", icons: ["🤫", "👂", "😌"] },
                { text: "Bé đi thuyền.", icons: ["👧", "⛵", "🌊"] },
                { text: "Tiếng chim.", icons: ["🐦", "🎶", "🎤"] },
                { text: "Yên lặng.", icons: ["🤫", "😌", "🤫"] },
                { text: "Thuyền.", icons: ["⛵", "⛵", "⛵"] },
                { text: "Tiếng.", icons: ["🔊", "📢", "🎶"] },
                { text: "Yên.", icons: ["🤫", "😌", "🤫"] },
                { text: "Thuyền.", icons: ["⛵", "⛵", "⛵"] },
                { text: "Tiếng.", icons: ["🔊", "📢", "🎶"] },
                { text: "Yên.", icons: ["🤫", "😌", "🤫"] },
                { text: "Thuyền.", icons: ["⛵", "⛵", "⛵"] },
                { text: "Tiếng.", icons: ["🔊", "📢", "🎶"] },
                { text: "Yên.", icons: ["🤫", "😌", "🤫"] },
                { text: "Thuyền.", icons: ["⛵", "⛵", "⛵"] },
                { text: "Tiếng.", icons: ["🔊", "📢", "🎶"] },
                { text: "Yên.", icons: ["🤫", "😌", "🤫"] },
                { text: "Thuyền.", icons: ["⛵", "⛵", "⛵"] },
                { text: "Tiếng.", icons: ["🔊", "📢", "🎶"] }
            ]},
            { id: "ƯƠNG", label: "ƯƠNG", title: "Bé Học Vần ƯƠNG", themeClass: "theme-uong", sentences: [
                { text: "Hướng dương quay về phía mặt trời.", icons: ["🌻", "☀️", "😊"] },
                { text: "Bé có một gương mặt dễ thương.", icons: ["👧", "😊", "💖"] },
                { text: "Con đường về nhà.", icons: ["🏡", "🛣️", "🚶"] },
                { text: "Gương soi của mẹ.", icons: ["🪞", "👩", "✨"] },
                { text: "Hướng.", icons: ["➡️", "⬅️", "⬆️"] },
                { text: "Gương.", icons: ["🪞", "🪞", "🪞"] },
                { text: "Đường.", icons: ["🛣️", "🛣️", "🛣️"] },
                { text: "Gương.", icons: ["🪞", "🪞", "🪞"] },
                { text: "Hướng.", icons: ["➡️", "⬅️", "⬆️"] },
                { text: "Gương.", icons: ["🪞", "🪞", "🪞"] },
                { text: "Đường.", icons: ["🛣️", "🛣️", "🛣️"] },
                { text: "Gương.", icons: ["🪞", "🪞", "🪞"] },
                { text: "Hướng.", icons: ["➡️", "⬅️", "⬆️"] },
                { text: "Gương.", icons: ["🪞", "🪞", "🪞"] },
                { text: "Đường.", icons: ["🛣️", "🛣️", "🛣️"] },
                { text: "Gương.", icons: ["🪞", "🪞", "🪞"] },
                { text: "Hướng.", icons: ["➡️", "⬅️", "⬆️"] },
                { text: "Gương.", icons: ["🪞", "🪞", "🪞"] },
                { text: "Đường.", icons: ["🛣️", "🛣️", "🛣️"] },
                { text: "Gương.", icons: ["🪞", "🪞", "🪞"] }
            ]},
            { id: "UÔNG", label: "UÔNG", title: "Bé Học Vần UÔNG", themeClass: "theme-uong-mo", sentences: [
                { text: "Uống nước thật nhiều.", icons: ["💧", "🥤", "😊"] },
                { text: "Chiếc luống rau.", icons: ["🥬", "🌱", "🌿"] },
                { text: "Bé uống nước.", icons: ["👧", "💧", "🥤"] },
                { text: "Cái luống.", icons: ["🥬", "🌱", "🌿"] },
                { text: "Bé uống.", icons: ["👧", "💧", "🥤"] },
                { text: "Luống.", icons: ["🥬", "🌱", "🌿"] },
                { text: "Bé uống.", icons: ["👧", "💧", "🥤"] },
                { text: "Luống.", icons: ["🥬", "🌱", "🌿"] },
                { text: "Bé uống.", icons: ["👧", "💧", "🥤"] },
                { text: "Luống.", icons: ["🥬", "🌱", "🌿"] },
                { text: "Bé uống.", icons: ["👧", "💧", "🥤"] },
                { text: "Luống.", icons: ["🥬", "🌱", "🌿"] },
                { text: "Bé uống.", icons: ["👧", "💧", "🥤"] },
                { text: "Luống.", icons: ["🥬", "🌱", "🌿"] },
                { text: "Bé uống.", icons: ["👧", "💧", "🥤"] },
                { text: "Luống.", icons: ["🥬", "🌱", "🌿"] },
                { text: "Bé uống.", icons: ["👧", "💧", "🥤"] },
                { text: "Luống.", icons: ["🥬", "🌱", "🌿"] },
                { text: "Bé uống.", icons: ["👧", "💧", "🥤"] },
                { text: "Luống.", icons: ["🥬", "🌱", "🌿"] }
            ]},
            { id: "UÔT", label: "UÔT", title: "Bé Học Vần UÔT", themeClass: "theme-uot", sentences: [
                { text: "Bé tuột tay.", icons: ["👦", "👋", "🤕"] },
                { text: "Bé tuột rồi.", icons: ["👧", "😔", "😞"] },
                { text: "Tuột.", icons: ["👦", "👋", "🤕"] },
                { text: "Tuột.", icons: ["👧", "😔", "😞"] },
                { text: "Tuột.", icons: ["👦", "👋", "🤕"] },
                { text: "Tuột.", icons: ["👧", "😔", "😞"] },
                { text: "Tuột.", icons: ["👦", "👋", "🤕"] },
                { text: "Tuột.", icons: ["👧", "😔", "😞"] },
                { text: "Tuột.", icons: ["👦", "👋", "🤕"] },
                { text: "Tuột.", icons: ["👧", "😔", "😞"] },
                { text: "Tuột.", icons: ["👦", "👋", "🤕"] },
                { text: "Tuột.", icons: ["👧", "😔", "😞"] },
                { text: "Tuột.", icons: ["👦", "👋", "🤕"] },
                { text: "Tuột.", icons: ["👧", "😔", "😞"] },
                { text: "Tuột.", icons: ["👦", "👋", "🤕"] },
                { text: "Tuột.", icons: ["👧", "😔", "😞"] },
                { text: "Tuột.", icons: ["👦", "👋", "🤕"] },
                { text: "Tuột.", icons: ["👧", "😔", "😞"] },
                { text: "Tuột.", icons: ["👦", "👋", "🤕"] },
                { text: "Tuột.", icons: ["👧", "😔", "😞"] }
            ]},
            { id: "OAI", label: "OAI", title: "Bé Học Vần OAI", themeClass: "theme-oai", sentences: [
                { text: "Bạn Oai rất giỏi.", icons: ["👦", "👍", "🏆"] },
                { text: "Oai phong, lẫm liệt.", icons: ["👑", "🦁", "💪"] },
                { text: "Bé oai oách.", icons: ["👧", "😠", "😤"] },
                { text: "Bạn Oai.", icons: ["👦", "👍", "🏆"] },
                { text: "Oai.", icons: ["👑", "🦁", "💪"] },
                { text: "Oai oách.", icons: ["😠", "😤", "😠"] },
                { text: "Bạn Oai.", icons: ["👦", "👍", "🏆"] },
                { text: "Oai.", icons: ["👑", "🦁", "💪"] },
                { text: "Oai oách.", icons: ["😠", "😤", "😠"] },
                { text: "Bạn Oai.", icons: ["👦", "👍", "🏆"] },
                { text: "Oai.", icons: ["👑", "🦁", "💪"] },
                { text: "Oai oách.", icons: ["😠", "😤", "😠"] },
                { text: "Bạn Oai.", icons: ["👦", "👍", "🏆"] },
                { text: "Oai.", icons: ["👑", "🦁", "💪"] },
                { text: "Oai oách.", icons: ["😠", "😤", "😠"] },
                { text: "Bạn Oai.", icons: ["👦", "👍", "🏆"] },
                { text: "Oai.", icons: ["👑", "🦁", "💪"] },
                { text: "Oai oách.", icons: ["😠", "😤", "😠"] },
                { text: "Bạn Oai.", icons: ["👦", "👍", "🏆"] },
                { text: "Oai.", icons: ["👑", "🦁", "💪"] }
            ]}
        ];

        let currentContentIndex = 0;
        let currentSentenceIndex = 0;

        // Audio for recording
        let mediaRecorder;
        let recordedAudioChunks = [];
        let recordedAudioBlob = null;
        let recording = false;
        
        // Timer
        let timer;
        let timeLeft = 90;
        let timerRunning = true;

        // DOM elements
        const sentenceDisplay = document.getElementById('sentence-display');
        const nextBtn = document.getElementById('next-btn');
        const prevBtn = document.getElementById('prev-btn');
        const readAloudBtn = document.getElementById('read-aloud-btn');
        const recordBtn = document.getElementById('record-btn');
        const playbackBtn = document.getElementById('playback-btn');
        const counter = document.getElementById('counter');
        const timerDisplay = document.getElementById('timer-display');
        const stopTimerBtn = document.getElementById('stop-timer-btn');
        const micStatus = document.getElementById('mic-status');
        const navContainer = document.getElementById('nav-container');
        const gameContainer = document.querySelector('.game-container');
        const body = document.querySelector('body');
        const gameTitle = document.getElementById('game-title');


        // Functions
        function renderNav() {
            navContainer.innerHTML = '';
            contentData.forEach((item, index) => {
                const button = document.createElement('button');
                button.textContent = item.label;
                button.classList.add('nav-btn');
                button.addEventListener('click', () => {
                    currentContentIndex = index;
                    currentSentenceIndex = 0;
                    updateUI();
                    updateNavActiveState();
                });
                navContainer.appendChild(button);
            });
            updateNavActiveState();
        }

        function updateNavActiveState() {
            const navButtons = navContainer.querySelectorAll('.nav-btn');
            navButtons.forEach((btn, index) => {
                if (index === currentContentIndex) {
                    btn.classList.add('active');
                } else {
                    btn.classList.remove('active');
                }
            });
        }

        function updateUI() {
            const currentContent = contentData[currentContentIndex];
            const currentSentence = currentContent.sentences[currentSentenceIndex];
            
            body.className = currentContent.themeClass;
            gameContainer.className = `game-container ${currentContent.themeClass}`;
            gameTitle.textContent = currentContent.title;

            sentenceDisplay.innerHTML = '';
            const words = currentSentence.text.split(' ');
            words.forEach((word, index) => {
                const span = document.createElement('span');
                span.textContent = word;
                sentenceDisplay.appendChild(span);

                if (index < words.length - 1) {
                    const iconIndex = index % currentSentence.icons.length;
                    const iconSpan = document.createElement('span');
                    iconSpan.textContent = currentSentence.icons[iconIndex];
                    iconSpan.classList.add('icon');
                    sentenceDisplay.appendChild(iconSpan);
                }
            });

            counter.textContent = `${currentSentenceIndex + 1}/${currentContent.sentences.length}`;
            resetTimer();
        }

        function resetTimer() {
            clearInterval(timer);
            timeLeft = 90;
            timerRunning = true;
            stopTimerBtn.textContent = 'Dừng lại';
            timerDisplay.textContent = `Thời gian còn lại: ${timeLeft}s`;
            timer = setInterval(() => {
                timeLeft--;
                timerDisplay.textContent = `Thời gian còn lại: ${timeLeft}s`;
                if (timeLeft <= 0) {
                    clearInterval(timer);
                    nextSentence();
                }
            }, 1000);
        }

        function toggleTimer() {
            if (timerRunning) {
                clearInterval(timer);
                stopTimerBtn.textContent = 'Tiếp tục';
            } else {
                resetTimer();
            }
            timerRunning = !timerRunning;
        }

        // Sound effect for navigation
        function playCuteSound() {
            try {
                const audioContext = new (window.AudioContext || window.webkitAudioContext)();
                const oscillator = audioContext.createOscillator();
                const gainNode = audioContext.createGain();

                oscillator.type = 'sine';
                oscillator.frequency.value = 440;
                gainNode.gain.setValueAtTime(0.5, audioContext.currentTime);

                oscillator.connect(gainNode);
                gainNode.connect(audioContext.destination);

                oscillator.start(audioContext.currentTime);
                oscillator.stop(audioContext.currentTime + 0.1);
            } catch (e) {
                console.warn("AudioContext not supported, can't play sound effect.");
            }
        }

        // --- Recording and Playback Logic ---

        // Asks for microphone permission and initializes MediaRecorder
        async function initRecorder() {
            if (!navigator.mediaDevices || !navigator.mediaDevices.getUserMedia) {
                micStatus.textContent = 'Trình duyệt không hỗ trợ ghi âm.';
                micStatus.classList.remove('hidden');
                recordBtn.disabled = true;
                return;
            }
            try {
                const stream = await navigator.mediaDevices.getUserMedia({ audio: true });
                mediaRecorder = new MediaRecorder(stream);
                mediaRecorder.ondataavailable = event => {
                    recordedAudioChunks.push(event.data);
                };
                mediaRecorder.onstop = () => {
                    recordedAudioBlob = new Blob(recordedAudioChunks, { type: 'audio/webm' });
                    playbackBtn.disabled = false;
                    recordBtn.textContent = 'Ghi âm lại';
                    recordBtn.classList.remove('recording');
                    recording = false;
                };
            } catch (err) {
                micStatus.textContent = 'Không thể truy cập microphone. Vui lòng cấp quyền ghi âm.';
                micStatus.classList.remove('hidden');
                recordBtn.disabled = true;
                console.error(`Microphone access denied: ${err}`);
            }
        }

        // Starts or stops the recording
        function toggleRecording() {
            if (!mediaRecorder) {
                console.error('Chức năng ghi âm chưa sẵn sàng. Vui lòng thử lại.');
                return;
            }

            if (!recording) {
                recordedAudioChunks = [];
                mediaRecorder.start();
                recordBtn.textContent = 'Đang ghi âm...';
                recordBtn.classList.add('recording');
                playbackBtn.disabled = true;
                recording = true;
            } else {
                mediaRecorder.stop();
            }
        }
        
        // Plays back the recorded audio
        function playRecording() {
            if (recordedAudioBlob) {
                const audioUrl = URL.createObjectURL(recordedAudioBlob);
                const audio = new Audio(audioUrl);
                audio.play();
            }
        }
        
        // --- AI TTS Logic ---
        
        function showLoading(show) {
            if (show) {
                LOADING_OVERLAY.style.display = 'flex';
                readAloudBtn.disabled = true;
                nextBtn.disabled = true;
                prevBtn.disabled = true;
            } else {
                LOADING_OVERLAY.style.display = 'none';
                readAloudBtn.disabled = false;
                nextBtn.disabled = false;
                prevBtn.disabled = false;
            }
        }
        
        async function readAloud() {
            showLoading(true);
            const textToRead = `Đọc chậm và rõ ràng như một người đang kể chuyện: ${contentData[currentContentIndex].sentences[currentSentenceIndex].text}`;
            const payload = {
                contents: [{
                    parts: [{ text: textToRead }]
                }],
                generationConfig: {
                    responseModalities: ["AUDIO"],
                    speechConfig: {
                        voiceConfig: {
                            prebuiltVoiceConfig: { voiceName: "Orus" }
                        }
                    }
                },
                model: "gemini-2.5-flash-preview-tts"
            };

            let retryCount = 0;
            const maxRetries = 5;

            while (retryCount < maxRetries) {
                try {
                    const response = await fetch(`${API_URL}${API_KEY}`, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });

                    if (!response.ok) {
                        if (response.status === 429) {
                            const delay = Math.pow(2, retryCount) * 1000;
                            retryCount++;
                            await new Promise(resolve => setTimeout(resolve, delay));
                            continue;
                        } else {
                             console.error("API error:", response.status, response.statusText);
                            break;
                        }
                    }

                    const result = await response.json();
                    const part = result?.candidates?.[0]?.content?.parts?.[0];

                    if (part?.inlineData?.data && part.inlineData.mimeType.startsWith("audio/")) {
                        const audioData = part.inlineData.data;
                        const mimeType = part.inlineData.mimeType;
                        const sampleRate = parseInt(mimeType.match(/rate=(\d+)/)[1], 10);
                        const pcmData = base64ToArrayBuffer(audioData);
                        const pcm16 = new Int16Array(pcmData);
                        const wavBlob = pcmToWav(pcm16, sampleRate);
                        const audioUrl = URL.createObjectURL(wavBlob);
                        const audio = new Audio(audioUrl);
                        audio.play();
                    } else {
                        console.error("Lỗi API: Dữ liệu âm thanh không hợp lệ hoặc bị thiếu.");
                    }
                    break; 

                } catch (error) {
                    console.error("Fetch error:", error);
                    break;
                }
            }
             showLoading(false);
        }

        // Helper functions for audio processing
        function base64ToArrayBuffer(base64) {
            const binaryString = window.atob(base64);
            const len = binaryString.length;
            const bytes = new Uint8Array(len);
            for (let i = 0; i < len; i++) {
                bytes[i] = binaryString.charCodeAt(i);
            }
            return bytes.buffer;
        }

        function pcmToWav(pcmData, sampleRate) {
            const numChannels = 1;
            const bitDepth = 16;
            const pcmLength = pcmData.byteLength;
            const wavLength = pcmLength + 44;
            const buffer = new ArrayBuffer(wavLength);
            const view = new DataView(buffer);

            let offset = 0;

            // RIFF header
            writeString(view, offset, 'RIFF'); offset += 4;
            view.setUint32(offset, wavLength - 8, true); offset += 4;
            writeString(view, offset, 'WAVE'); offset += 4;

            // FMT sub-chunk
            writeString(view, offset, 'fmt '); offset += 4;
            view.setUint32(offset, 16, true); offset += 4; // Sub-chunk size
            view.setUint16(offset, 1, true); offset += 2; // Audio format (1 = PCM)
            view.setUint16(offset, numChannels, true); offset += 2;
            view.setUint32(offset, sampleRate, true); offset += 4;
            view.setUint32(offset, sampleRate * numChannels * (bitDepth / 8), true); offset += 4;
            view.setUint16(offset, numChannels * (bitDepth / 8), true); offset += 2;
            view.setUint16(offset, bitDepth, true); offset += 2;

            // DATA sub-chunk
            writeString(view, offset, 'data'); offset += 4;
            view.setUint32(offset, pcmLength, true); offset += 4;

            // Write PCM data
            const pcmView = new Uint8Array(pcmData.buffer);
            for (let i = 0; i < pcmLength; i++, offset++) {
                view.setUint8(offset, pcmView[i]);
            }

            return new Blob([view], { type: 'audio/wav' });
        }

        function writeString(view, offset, string) {
            for (let i = 0; i < string.length; i++) {
                view.setUint8(offset + i, string.charCodeAt(i));
            }
        }
        
        // Event handlers
        function nextSentence() {
            playCuteSound();
            const currentContent = contentData[currentContentIndex];
            currentSentenceIndex = (currentSentenceIndex + 1) % currentContent.sentences.length;
            updateUI();
        }

        function prevSentence() {
            playCuteSound();
            const currentContent = contentData[currentContentIndex];
            currentSentenceIndex = (currentSentenceIndex - 1 + currentContent.sentences.length) % currentContent.sentences.length;
            updateUI();
        }

        // Event listeners
        document.addEventListener('DOMContentLoaded', () => {
            renderNav();
            updateUI();
            initRecorder();
            authenticate();
        });

        nextBtn.addEventListener('click', nextSentence);
        prevBtn.addEventListener('click', prevSentence);
        readAloudBtn.addEventListener('click', readAloud);
        recordBtn.addEventListener('click', toggleRecording);
        playbackBtn.addEventListener('click', playRecording);
        stopTimerBtn.addEventListener('click', toggleTimer);
    </script>
</body>
</html>
