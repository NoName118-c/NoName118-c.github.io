<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Carnatic Music Notation Composer</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: white;
            border-radius: 15px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            overflow: hidden;
        }
        
        .header {
            background: linear-gradient(135deg, #ff6b6b, #ee5a24);
            color: white;
            padding: 30px;
            text-align: center;
        }
        
        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }
        
        .header p {
            font-size: 1.2em;
            opacity: 0.9;
        }
        
        .composition-info {
            padding: 30px;
            background: #f8f9fa;
            border-bottom: 2px solid #e9ecef;
        }
        
        .info-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
        }
        
        .form-group {
            display: flex;
            flex-direction: column;
        }
        
        .form-group label {
            font-weight: 600;
            margin-bottom: 8px;
            color: #495057;
        }
        
        .form-group input {
            padding: 12px;
            border: 2px solid #dee2e6;
            border-radius: 8px;
            font-size: 16px;
            transition: border-color 0.3s ease;
        }
        
        .form-group input:focus {
            outline: none;
            border-color: #007bff;
            box-shadow: 0 0 0 3px rgba(0,123,255,0.25);
        }
        
        .controls {
            padding: 30px;
            background: white;
            border-bottom: 2px solid #e9ecef;
        }
        
        .control-section {
            margin-bottom: 25px;
        }
        
        .control-section h3 {
            color: #495057;
            margin-bottom: 15px;
            font-size: 1.3em;
        }
        
        .control-row {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            align-items: end;
        }
        
        .input-group {
            display: flex;
            flex-direction: column;
            min-width: 120px;
        }
        
        .input-group label {
            font-weight: 500;
            margin-bottom: 5px;
            color: #6c757d;
        }
        
        .input-group input, .input-group select {
            padding: 10px;
            border: 2px solid #dee2e6;
            border-radius: 6px;
            font-size: 14px;
        }
        
        .btn {
            padding: 10px 20px;
            border: none;
            border-radius: 6px;
            font-size: 14px;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }
        
        .btn-primary {
            background: linear-gradient(135deg, #007bff, #0056b3);
            color: white;
        }
        
        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,123,255,0.4);
        }
        
        .btn-secondary {
            background: linear-gradient(135deg, #6c757d, #495057);
            color: white;
        }
        
        .btn-secondary:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(108,117,125,0.4);
        }
        
        .btn-success {
            background: linear-gradient(135deg, #28a745, #1e7e34);
            color: white;
        }
        
        .btn-success:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(40,167,69,0.4);
        }
        
        .btn-danger {
            background: linear-gradient(135deg, #dc3545, #c82333);
            color: white;
        }
        
        .btn-danger:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(220,53,69,0.4);
        }
        
        .btn-warning {
            background: linear-gradient(135deg, #ffc107, #e0a800);
            color: #212529;
        }
        
        .btn-warning:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(255,193,7,0.4);
        }
        
        .punctuation-buttons {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }
        
        .punct-btn {
            padding: 8px 12px;
            background: #f8f9fa;
            border: 2px solid #dee2e6;
            border-radius: 4px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.2s ease;
        }
        
        .punct-btn:hover {
            background: #e9ecef;
            border-color: #adb5bd;
        }
        
        .notation-area {
            padding: 30px;
            background: #ffffff;
            min-height: 400px;
        }
        
        .notation-row {
            margin-bottom: 30px;
            padding: 20px;
            border: 2px solid #e9ecef;
            border-radius: 10px;
            background: #f8f9fa;
            transition: all 0.3s ease;
        }
        
        .notation-row:hover {
            border-color: #007bff;
            box-shadow: 0 5px 15px rgba(0,123,255,0.1);
        }
        
        .row-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 1px solid #dee2e6;
        }
        
        .row-number {
            font-weight: bold;
            color: #495057;
            font-size: 1.1em;
        }
        
        .row-controls {
            display: flex;
            gap: 10px;
        }
        
        .swaram-line {
            min-height: 50px;
            padding: 15px;
            background: white;
            border: 2px dashed #dee2e6;
            border-radius: 8px;
            margin-bottom: 15px;
            line-height: 1.8;
            font-size: 18px;
            font-weight: 500;
        }
        
        .sahityam-line {
            min-height: 40px;
            padding: 15px;
            background: #fff3cd;
            border: 2px dashed #ffeaa7;
            border-radius: 8px;
            line-height: 1.6;
            font-size: 16px;
            font-style: italic;
        }
        
        .swaram {
            display: inline-block;
            position: relative;
            margin: 0 8px 5px 0;
            padding: 5px 8px;
            background: linear-gradient(135deg, #74b9ff, #0984e3);
            color: white;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.2s ease;
        }
        
        .swaram:hover {
            transform: translateY(-2px);
            box-shadow: 0 3px 10px rgba(116,185,255,0.4);
        }
        
        .octave-dot-high {
            position: absolute;
            top: -3px;
            right: 2px;
            width: 4px;
            height: 4px;
            background: #ff6b6b;
            border-radius: 50%;
        }
        
        .octave-dot-low {
            position: absolute;
            bottom: -3px;
            right: 2px;
            width: 4px;
            height: 4px;
            background: #ff6b6b;
            border-radius: 50%;
        }
        
        .action-buttons {
            padding: 30px;
            background: #f8f9fa;
            text-align: center;
            border-top: 2px solid #e9ecef;
        }
        
        .action-buttons .btn {
            margin: 0 10px;
            padding: 15px 30px;
            font-size: 16px;
        }
        
        .keyboard-shortcuts {
            margin-top: 20px;
            padding: 15px;
            background: #e9ecef;
            border-radius: 8px;
            font-size: 12px;
            color: #6c757d;
        }
        
        .keyboard-shortcuts h4 {
            margin-bottom: 10px;
            color: #495057;
        }
        
        .shortcut {
            display: inline-block;
            margin-right: 20px;
            margin-bottom: 5px;
        }
        
        .shortcut kbd {
            background: #495057;
            color: white;
            padding: 2px 6px;
            border-radius: 3px;
            font-size: 11px;
        }
        
        @media (max-width: 768px) {
            .container {
                margin: 10px;
                border-radius: 10px;
            }
            
            .header {
                padding: 20px;
            }
            
            .header h1 {
                font-size: 2em;
            }
            
            .composition-info, .controls, .notation-area {
                padding: 20px;
            }
            
            .control-row {
                flex-direction: column;
                align-items: stretch;
            }
            
            .input-group {
                min-width: auto;
            }
            
            .row-header {
                flex-direction: column;
                gap: 10px;
                align-items: stretch;
            }
            
            .row-controls {
                justify-content: center;
            }
            
            .action-buttons .btn {
                display: block;
                margin: 10px auto;
                width: 100%;
                max-width: 300px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🎵 Carnatic Music Notation Composer</h1>
            <p>Create beautiful Carnatic music compositions with swarams and sahityam</p>
        </div>
        
        <div class="composition-info">
            <div class="info-grid">
                <div class="form-group">
                    <label for="composition-title">Composition Title</label>
                    <input type="text" id="composition-title" placeholder="Enter composition title">
                </div>
                <div class="form-group">
                    <label for="raga">Raga</label>
                    <input type="text" id="raga" placeholder="Enter raga name">
                </div>
                <div class="form-group">
                    <label for="tala">Tala</label>
                    <input type="text" id="tala" placeholder="Enter tala name">
                </div>
                <div class="form-group">
                    <label for="composer">Composer</label>
                    <input type="text" id="composer" placeholder="Enter composer name">
                </div>
            </div>
        </div>
        
        <div class="controls">
            <div class="control-section">
                <h3>Add Swarams</h3>
                <div
