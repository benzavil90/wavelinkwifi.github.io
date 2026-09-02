<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Status Confirmation</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f6f9;
            display: flex;
            justify-content: center;
            align-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
        }

        .card {
            background: #ffffff;
            border-radius: 12px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            max-width: 400px;
            width: 90%;
            padding: 24px;
            text-align: center;
        }

        .status-icon {
            width: 48px;
            height: 48px;
            background-color: #e6f4ea;
            color: #137333;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 16px auto;
            font-size: 24px;
            font-weight: bold;
        }

        .title {
            font-size: 1.25rem;
            color: #202124;
            margin-bottom: 8px;
        }

        .description {
            font-size: 0.9rem;
            color: #5f6368;
            margin-bottom: 24px;
        }

        .action-button {
            display: inline-block;
            width: 100%;
            padding: 12px 0;
            background-color: #1a73e8;
            color: #ffffff;
            border: none;
            border-radius: 6px;
            font-size: 1rem;
            text-decoration: none;
            cursor: pointer;
        }

        .action-button:hover {
            background-color: #1557b0;
        }
    </style>
</head>
<body>

    <div class="card">
        <div class="status-icon">✓</div>
        <h1 class="title">Action Complete</h1>
        <p class="description">Your request has been processed successfully.</p>
        <a href="#" class="action-button">Continue</a>
    </div>

</body>
</html>
