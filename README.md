<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TL服务中心 - 高级黑金风格</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700&family=Raleway:wght@400;600&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Raleway', 'Microsoft YaHei', sans-serif;
        }

        :root {
            --black-1: #0a0a0a;
            --black-2: #121212;
            --black-3: #1a1a1a;
            --gold-1: #c6a755;
            --gold-2: #d4af37;
            --gold-3: #e6d6a9;
            --light-gold: #f5f0e1;
            --glow: 0 0 15px rgba(212, 175, 55, 0.6);
            --error-red: #ff3860;
            --error-glow: 0 0 10px rgba(255, 56, 96, 0.7);
            --green-glow: 0 0 15px rgba(76, 175, 80, 0.6);
            --transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        body {
            background: radial-gradient(ellipse at center, #070707 0%, #000 100%);
            color: var(--light-gold);
            min-height: 100vh;
            position: relative;
            overflow-x: hidden;
            line-height: 1.7;
        }

        /* 高级粒子背景效果 */
        .particle-layer {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            pointer-events: none;
            overflow: hidden;
        }

        .gold-particle {
            position: absolute;
            border-radius: 50%;
            opacity: 0;
            animation: twinkle 5s infinite;
        }
        
        /* 金色光束效果 */
        .light-beam {
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            background: radial-gradient(circle at 30% 20%, rgba(212, 175, 55, 0.1), transparent 70%);
            pointer-events: none;
            z-index: -1;
            opacity: 0.8;
        }

        /* 顶部导航 */
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 25px 40px;
            position: relative;
            z-index: 20;
            animation: slideDown 0.8s ease-out;
        }

        .logo {
            font-family: 'Playfair Display', serif;
            font-size: 36px;
            font-weight: 800;
            letter-spacing: 3px;
            text-transform: uppercase;
            color: transparent;
            background: linear-gradient(90deg, var(--gold-3), var(--gold-2), var(--gold-3));
            -webkit-background-clip: text;
            background-clip: text;
            text-shadow: var(--glow);
            position: relative;
            transition: var(--transition);
        }

        .logo:hover {
            text-shadow: 0 0 25px rgba(212, 175, 55, 0.8);
            transform: scale(1.05);
        }

        .logo span {
            color: var(--gold-2);
        }

        /* 主标题 */
        .hero {
            text-align: center;
            padding: 40px 20px 60px;
            position: relative;
            z-index: 10;
            animation: fadeInUp 1s ease-out;
        }

        .hero h1 {
            font-family: 'Playfair Display', serif;
            font-size: 64px;
            font-weight: 800;
            letter-spacing: 6px;
            text-transform: uppercase;
            margin-bottom: 20px;
            background: linear-gradient(90deg, var(--gold-3), var(--gold-2), var(--gold-1));
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-shadow: 0 0 30px rgba(212, 175, 55, 0.6);
            position: relative;
            display: inline-block;
        }
        
        .hero h1::after {
            content: '';
            position: absolute;
            bottom: -15px;
            left: 50%;
            transform: translateX(-50%);
            width: 200px;
            height: 4px;
            background: linear-gradient(90deg, transparent, var(--gold-2), transparent);
            border-radius: 2px;
        }

        /* 服务卡片 */
        .services-container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px 60px;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
            gap: 35px;
            position: relative;
            z-index: 10;
        }

        .service-card {
            background: linear-gradient(145deg, rgba(26, 26, 26, 0.7), rgba(10, 10, 10, 0.8));
            border: 1px solid rgba(198, 167, 85, 0.2);
            border-radius: 25px;
            padding: 45px 30px;
            text-align: center;
            transition: var(--transition);
            box-shadow: 0 15px 40px rgba(0, 0, 0, 0.7);
            position: relative;
            overflow: hidden;
            backdrop-filter: blur(12px);
            cursor: pointer;
            transform: translateY(0);
        }

        .service-card::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 5px;
            background: linear-gradient(90deg, transparent, var(--gold-2), transparent);
            opacity: 0;
            transition: opacity 0.4s ease;
        }
        
        .service-card::after {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(600px circle at var(--mouse-x) var(--mouse-y), 
                        rgba(212, 175, 55, 0.1), transparent 40%);
            z-index: -1;
            opacity: 0;
            transition: opacity 0.4s ease;
        }

        .service-card:hover {
            transform: translateY(-15px);
            border-color: var(--gold-2);
            box-shadow: 0 25px 60px rgba(198, 167, 85, 0.3);
        }
        
        .service-card:hover::after {
            opacity: 1;
        }

        .service-card:hover::before {
            opacity: 1;
        }

        .service-icon {
            width: 100px;
            height: 100px;
            margin: 0 auto 30px;
            background: rgba(198, 167, 85, 0.08);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 45px;
            color: var(--gold-2);
            border: 2px solid var(--gold-2);
            box-shadow: 0 0 30px rgba(198, 167, 85, 0.25);
            transition: var(--transition);
            position: relative;
            z-index: 2;
        }

        .service-card:hover .service-icon {
            transform: scale(1.15) rotate(5deg);
            box-shadow: 0 0 50px rgba(212, 175, 55, 0.6);
            color: var(--gold-3);
            background: rgba(10, 10, 10, 0.3);
        }

        .service-card h3 {
            font-size: 26px;
            margin-bottom: 20px;
            color: var(--gold-3);
            letter-spacing: 1px;
            transition: var(--transition);
        }
        
        .service-card:hover h3 {
            color: var(--gold-2);
            text-shadow: 0 0 10px rgba(212, 175, 55, 0.5);
        }

        .service-card p {
            color: var(--gold-3);
            opacity: 0.8;
            font-size: 17px;
            max-width: 280px;
            margin: 0 auto;
            line-height: 1.8;
            transition: var(--transition);
        }
        
        .service-card:hover p {
            opacity: 1;
            transform: translateY(5px);
        }

        /* 页面内容 */
        .page {
            display: none;
            position: relative;
            z-index: 10;
            max-width: 850px;
            margin: 0 auto;
            padding: 30px 20px 80px;
            animation: fadeIn 0.6s ease;
        }

        .active {
            display: block;
        }

        .card {
            background: linear-gradient(145deg, rgba(26, 26, 26, 0.75), rgba(10, 10, 10, 0.85));
            border: 1px solid rgba(198, 167, 85, 0.25);
            border-radius: 25px;
            padding: 50px 40px;
            margin: 20px auto;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.8);
            position: relative;
            overflow: hidden;
            backdrop-filter: blur(15px);
            transition: var(--transition);
            transform: scale(1);
        }
        
        .card:hover {
            box-shadow: 0 25px 60px rgba(198, 167, 85, 0.2);
            border: 1px solid rgba(198, 167, 85, 0.4);
            transform: scale(1.005);
        }

        .card::before {
            content: "";
            position: absolute;
            top: -2px;
            left: -2px;
            right: -2px;
            bottom: -2px;
            background: linear-gradient(45deg, var(--gold-1), var(--gold-2), var(--gold-1));
            z-index: -1;
            border-radius: 27px;
            opacity: 0.15;
        }
        
        .card::after {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(600px circle at var(--mouse-x) var(--mouse-y), 
                        rgba(212, 175, 55, 0.05), transparent 40%);
            z-index: -1;
            opacity: 0;
            transition: opacity 0.4s ease;
        }
        
        .card:hover::after {
            opacity: 1;
        }

        .card-title {
            text-align: center;
            margin-bottom: 45px;
            position: relative;
            padding-bottom: 25px;
        }

        .card-title h2 {
            font-family: 'Playfair Display', serif;
            font-size: 40px;
            color: var(--gold-2);
            font-weight: 700;
            letter-spacing: 2px;
            text-shadow: var(--glow);
            position: relative;
            display: inline-block;
        }
        
        .card-title h2::after {
            content: '';
            position: absolute;
            bottom: -15px;
            left: 50%;
            transform: translateX(-50%);
            width: 100px;
            height: 3px;
            background: linear-gradient(90deg, transparent, var(--gold-2), transparent);
            border-radius: 2px;
        }

        /* 表单样式 */
        .form-group {
            margin-bottom: 30px;
            position: relative;
        }

        .form-group label {
            display: block;
            margin-bottom: 12px;
            font-weight: 600;
            color: var(--gold-2);
            font-size: 18px;
            letter-spacing: 0.5px;
        }

        .form-control {
            width: 100%;
            padding: 18px 25px;
            background: rgba(30, 30, 30, 0.6);
            border: 1px solid rgba(198, 167, 85, 0.25);
            border-radius: 12px;
            color: var(--light-gold);
            font-size: 17px;
            transition: var(--transition);
        }

        .form-control:focus {
            outline: none;
            border-color: var(--gold-2);
            box-shadow: 0 0 20px rgba(198, 167, 85, 0.4);
            background: rgba(30, 30, 30, 0.8);
        }
        
        .form-control:hover {
            border-color: var(--gold-1);
        }

        /* 单选按钮组 */
        .radio-group {
            display: flex;
            gap: 30px;
            margin-top: 10px;
        }
        
        .radio-option {
            display: flex;
            align-items: center;
            gap: 8px;
            padding: 10px 15px;
            border-radius: 10px;
            transition: var(--transition);
            background: rgba(30, 30, 30, 0.4);
        }
        
        .radio-option:hover {
            background: rgba(212, 175, 55, 0.1);
            transform: translateY(-3px);
        }
        
        .radio-option input[type="radio"] {
            width: 20px;
            height: 20px;
            accent-color: var(--gold-2);
        }
        
        .radio-option label {
            margin: 0;
            font-size: 17px;
            color: var(--gold-3);
        }

        /* 按钮样式 */
        .btn {
            padding: 18px 35px;
            border: none;
            border-radius: 50px;
            font-size: 19px;
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
            position: relative;
            overflow: hidden;
            background: linear-gradient(90deg, var(--gold-1), var(--gold-2));
            color: var(--black-1);
            display: block;
            width: 100%;
            max-width: 350px;
            margin: 40px auto 0;
            box-shadow: 0 8px 25px rgba(198, 167, 85, 0.4);
            letter-spacing: 1px;
            z-index: 2;
        }
        
        .btn::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, var(--gold-2), var(--gold-1));
            opacity: 0;
            transition: opacity 0.4s ease;
            z-index: -1;
        }

        .btn:hover {
            transform: translateY(-8px) scale(1.05);
            box-shadow: 0 15px 35px rgba(198, 167, 85, 0.6);
            color: var(--black-1);
        }
        
        .btn:hover::before {
            opacity: 1;
        }

        .btn:active {
            transform: translateY(2px);
        }

        /* 返回按钮 */
        .back-btn {
            position: absolute;
            top: 35px;
            left: 35px;
            color: var(--gold-3);
            font-size: 26px;
            cursor: pointer;
            transition: var(--transition);
            z-index: 100;
            background: rgba(10, 10, 10, 0.7);
            width: 55px;
            height: 55px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 1px solid rgba(198, 167, 85, 0.3);
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.6);
        }

        .back-btn:hover {
            color: var(--gold-2);
            background: rgba(198, 167, 85, 0.1);
            transform: translateX(-8px) rotate(-10deg);
            box-shadow: 0 0 30px rgba(212, 175, 55, 0.4);
        }

        /* 模态框 */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.95);
            z-index: 1000;
            justify-content: center;
            align-items: center;
            animation: fadeIn 0.4s ease;
        }

        .modal-content {
            background: linear-gradient(145deg, rgba(26, 26, 26, 0.95), rgba(10, 10, 10, 0.98));
            border: 1px solid var(--gold-1);
            border-radius: 25px;
            padding: 45px;
            max-width: 550px;
            width: 90%;
            box-shadow: 0 0 60px rgba(198, 167, 85, 0.4);
            position: relative;
            max-height: 90vh;
            overflow-y: auto;
            animation: scaleIn 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .close-modal {
            position: absolute;
            top: 25px;
            right: 25px;
            color: var(--gold-3);
            font-size: 30px;
            cursor: pointer;
            transition: var(--transition);
            width: 45px;
            height: 45px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .close-modal:hover {
            color: var(--gold-2);
            background: rgba(198, 167, 85, 0.1);
            transform: rotate(90deg) scale(1.1);
        }

        .modal-title {
            text-align: center;
            margin-bottom: 35px;
            color: var(--gold-2);
            font-size: 28px;
            font-weight: 700;
            font-family: 'Playfair Display', serif;
            text-shadow: var(--glow);
        }

        /* 支付方式 */
        .payment-options {
            display: flex;
            justify-content: center;
            gap: 35px;
            margin: 45px 0;
            flex-wrap: wrap;
        }

        .payment-option {
            text-align: center;
            padding: 30px;
            border: 1px solid rgba(198, 167, 85, 0.25);
            border-radius: 18px;
            cursor: pointer;
            transition: var(--transition);
            width: 170px;
            background: rgba(20, 20, 20, 0.7);
            position: relative;
            overflow: hidden;
        }
        
        .payment-option::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(200px circle at var(--mouse-x) var(--mouse-y), 
                        rgba(212, 175, 55, 0.1), transparent 70%);
            z-index: 1;
            opacity: 0;
            transition: opacity 0.4s ease;
        }

        .payment-option:hover {
            background: rgba(198, 167, 85, 0.12);
            border-color: var(--gold-2);
            transform: translateY(-10px) scale(1.05);
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.4);
        }
        
        .payment-option:hover::before {
            opacity: 1;
        }

        .payment-option i {
            font-size: 55px;
            margin-bottom: 25px;
            color: var(--gold-2);
            transition: var(--transition);
            position: relative;
            z-index: 2;
        }
        
        .payment-option:hover i {
            transform: scale(1.2) rotate(5deg);
            color: var(--gold-3);
        }

        .payment-option p {
            font-size: 20px;
            color: var(--gold-3);
            transition: var(--transition);
            position: relative;
            z-index: 2;
        }
        
        .payment-option:hover p {
            color: var(--gold-2);
            text-shadow: 0 0 8px rgba(212, 175, 55, 0.4);
        }

        /* 凭证上传 */
        .upload-area {
            border: 2px dashed rgba(198, 167, 85, 0.25);
            border-radius: 18px;
            padding: 45px 25px;
            text-align: center;
            margin: 35px 0;
            transition: var(--transition);
            cursor: pointer;
            background: rgba(20, 20, 20, 0.5);
            position: relative;
            overflow: hidden;
        }
        
        .upload-area::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(400px circle at var(--mouse-x) var(--mouse-y), 
                        rgba(212, 175, 55, 0.1), transparent 70%);
            z-index: 1;
            opacity: 0;
            transition: opacity 0.4s ease;
        }

        .upload-area:hover {
            border-color: var(--gold-2);
            background: rgba(198, 167, 85, 0.08);
            transform: translateY(-5px);
        }
        
        .upload-area:hover::before {
            opacity: 1;
        }

        .upload-area i {
            font-size: 65px;
            color: var(--gold-2);
            margin-bottom: 25px;
            transition: var(--transition);
            position: relative;
            z-index: 2;
        }
        
        .upload-area:hover i {
            transform: scale(1.1) rotate(5deg);
            color: var(--gold-3);
        }

        .upload-area h4 {
            font-size: 24px;
            color: var(--gold-3);
            margin-bottom: 15px;
            transition: var(--transition);
            position: relative;
            z-index: 2;
        }
        
        .upload-area:hover h4 {
            color: var(--gold-2);
            text-shadow: 0 0 8px rgba(212, 175, 55, 0.4);
        }

        .upload-area p {
            color: var(--gold-3);
            opacity: 0.7;
            font-size: 17px;
            transition: var(--transition);
            position: relative;
            z-index: 2;
        }
        
        .upload-area:hover p {
            opacity: 1;
        }

        /* 生日祝贺页面 */
        .birthday-card {
            text-align: center;
            padding: 40px 0 60px;
        }

        .birthday-title {
            font-family: 'Playfair Display', serif;
            font-size: 48px;
            color: var(--gold-2);
            margin-bottom: 40px;
            text-shadow: 0 0 30px rgba(212, 175, 55, 0.8);
            letter-spacing: 3px;
            position: relative;
            display: inline-block;
        }
        
        .birthday-title::after {
            content: '';
            position: absolute;
            bottom: -15px;
            left: 50%;
            transform: translateX(-50%);
            width: 200px;
            height: 3px;
            background: linear-gradient(90deg, transparent, var(--gold-2), transparent);
            border-radius: 2px;
        }

        .gift-icon {
            font-size: 90px;
            color: var(--gold-2);
            margin-bottom: 40px;
            text-shadow: var(--glow);
            animation: pulse 3s infinite, float 4s ease-in-out infinite;
        }

        .voucher-code {
            background: linear-gradient(90deg, rgba(198,167,85,0.12), rgba(212,175,55,0.18), rgba(198,167,85,0.12));
            padding: 30px;
            border-radius: 18px;
            margin: 50px auto;
            max-width: 500px;
            border: 1px solid var(--gold-2);
            transition: var(--transition);
            position: relative;
            overflow: hidden;
        }
        
        .voucher-code::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(400px circle at var(--mouse-x) var(--mouse-y), 
                        rgba(212, 175, 55, 0.15), transparent 70%);
            z-index: 1;
            opacity: 0;
            transition: opacity 0.4s ease;
        }
        
        .voucher-code:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.3);
        }
        
        .voucher-code:hover::before {
            opacity: 1;
        }

        .voucher-title {
            color: var(--gold-3);
            margin-bottom: 25px;
            font-size: 26px;
            letter-spacing: 1px;
            transition: var(--transition);
            position: relative;
            z-index: 2;
        }
        
        .voucher-code:hover .voucher-title {
            color: var(--gold-2);
            text-shadow: 0 0 8px rgba(212, 175, 55, 0.4);
        }

        .code-display {
            font-size: 42px;
            letter-spacing: 5px;
            color: var(--gold-3);
            font-weight: 800;
            background: rgba(10, 10, 10, 0.7);
            padding: 20px;
            border-radius: 12px;
            border: 1px solid var(--gold-2);
            font-family: monospace;
            transition: var(--transition);
            position: relative;
            z-index: 2;
        }
        
        .voucher-code:hover .code-display {
            transform: scale(1.02);
            box-shadow: 0 0 20px rgba(212, 175, 55, 0.3);
        }

        .quote {
            font-style: italic;
            margin-top: 60px;
            color: var(--gold-3);
            font-size: 22px;
            max-width: 700px;
            margin: 60px auto 0;
            text-shadow: 0 0 20px rgba(212, 175, 55, 0.6);
            position: relative;
            padding: 0 20px;
            transition: var(--transition);
        }
        
        .quote:hover {
            transform: translateY(-5px);
            color: var(--gold-2);
        }

        .quote::before, .quote::after {
            content: """;
            font-size: 60px;
            color: var(--gold-2);
            opacity: 0.3;
            position: absolute;
            transition: var(--transition);
        }

        .quote::before {
            top: -30px;
            left: -10px;
        }

        .quote::after {
            bottom: -50px;
            right: -10px;
            transform: rotate(180deg);
        }
        
        .quote:hover::before, .quote:hover::after {
            opacity: 0.5;
        }

        /* 联系问题选择 */
        .issues-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px;
            margin: 40px 0;
        }

        .issue-card {
            background: rgba(30, 30, 30, 0.6);
            border: 1px solid rgba(198, 167, 85, 0.2);
            border-radius: 15px;
            padding: 25px;
            text-align: center;
            cursor: pointer;
            transition: var(--transition);
            position: relative;
            overflow: hidden;
        }
        
        .issue-card::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(300px circle at var(--mouse-x) var(--mouse-y), 
                        rgba(212, 175, 55, 0.1), transparent 70%);
            z-index: 1;
            opacity: 0;
            transition: opacity 0.4s ease;
        }

        .issue-card:hover {
            background: rgba(198, 167, 85, 0.1);
            border-color: var(--gold-2);
            transform: translateY(-8px);
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.4);
        }
        
        .issue-card:hover::before {
            opacity: 1;
        }

        .issue-card i {
            font-size: 40px;
            color: var(--gold-2);
            margin-bottom: 20px;
            transition: var(--transition);
            position: relative;
            z-index: 2;
        }
        
        .issue-card:hover i {
            transform: scale(1.2) rotate(5deg);
            color: var(--gold-3);
        }

        .issue-card h4 {
            font-size: 20px;
            color: var(--gold-3);
            margin-bottom: 15px;
            transition: var(--transition);
            position: relative;
            z-index: 2;
        }
        
        .issue-card:hover h4 {
            color: var(--gold-2);
            text-shadow: 0 0 8px rgba(212, 175, 55, 0.4);
        }

        .issue-card p {
            color: var(--gold-3);
            opacity: 0.8;
            font-size: 16px;
            transition: var(--transition);
            position: relative;
            z-index: 2;
        }
        
        .issue-card:hover p {
            opacity: 1;
        }

        /* 通行证页面 */
        .passport-card {
            text-align: center;
            padding: 40px 0 60px;
        }

        .passport-title {
            font-family: 'Playfair Display', serif;
            font-size: 48px;
            color: var(--gold-2);
            margin-bottom: 40px;
            text-shadow: 0 0 30px rgba(212, 175, 55, 0.8);
            letter-spacing: 2px;
        }

        .passport-icon {
            font-size: 100px;
            color: var(--gold-2);
            margin-bottom: 40px;
            text-shadow: var(--glow);
            animation: pulse 3s infinite, float 4s ease-in-out infinite;
        }

        .passport-details {
            background: linear-gradient(90deg, rgba(198,167,85,0.1), rgba(212,175,55,0.15));
            padding: 30px;
            border-radius: 18px;
            margin: 40px auto;
            max-width: 500px;
            border: 1px solid var(--gold-2);
            text-align: left;
            transition: var(--transition);
            position: relative;
            overflow: hidden;
        }
        
        .passport-details::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(400px circle at var(--mouse-x) var(--mouse-y), 
                        rgba(212, 175, 55, 0.15), transparent 70%);
            z-index: 1;
            opacity: 0;
            transition: opacity 0.4s ease;
        }
        
        .passport-details:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.3);
        }
        
        .passport-details:hover::before {
            opacity: 1;
        }

        .passport-row {
            display: flex;
            justify-content: space-between;
            padding: 15px 0;
            border-bottom: 1px solid rgba(212, 175, 55, 0.2);
            transition: var(--transition);
            position: relative;
            z-index: 2;
        }
        
        .passport-row:hover {
            background: rgba(10, 10, 10, 0.3);
        }

        .passport-row:last-child {
            border-bottom: none;
        }

        .passport-label {
            color: var(--gold-3);
            font-weight: 600;
            flex: 1;
            transition: var(--transition);
        }
        
        .passport-row:hover .passport-label {
            color: var(--gold-2);
        }

        .passport-value {
            color: var(--gold-3);
            flex: 2;
            text-align: right;
            font-family: monospace;
            transition: var(--transition);
        }
        
        .passport-row:hover .passport-value {
            color: var(--gold-2);
            text-shadow: 0 0 5px rgba(212, 175, 55, 0.3);
        }

        .passport-code {
            font-size: 36px;
            letter-spacing: 5px;
            color: var(--gold-3);
            font-weight: 800;
            background: rgba(10, 10, 10, 0.7);
            padding: 20px;
            border-radius: 12px;
            border: 1px solid var(--gold-2);
            font-family: monospace;
            margin: 30px auto;
            max-width: 500px;
            transition: var(--transition);
            position: relative;
            overflow: hidden;
        }
        
        .passport-code::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(400px circle at var(--mouse-x) var(--mouse-y), 
                        rgba(212, 175, 55, 0.15), transparent 70%);
            z-index: 1;
            opacity: 0;
            transition: opacity 0.4s ease;
        }
        
        .passport-code:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.3);
        }
        
        .passport-code:hover::before {
            opacity: 1;
        }

        /* 错误提示 */
        .error-message {
            background: linear-gradient(135deg, rgba(255, 56, 96, 0.2), rgba(180, 20, 60, 0.3));
            border: 1px solid var(--gold-2);
            border-radius: 12px;
            padding: 15px 25px;
            margin: 25px 0;
            text-align: center;
            color: #fff;
            font-weight: 600;
            animation: pulseError 1.5s infinite;
            box-shadow: var(--error-glow);
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            transition: var(--transition);
        }
        
        .error-message:hover {
            transform: translateY(-3px);
            box-shadow: 0 0 20px rgba(255, 56, 96, 0.8);
        }

        .error-message i {
            font-size: 24px;
            color: #fff;
            text-shadow: 0 0 10px rgba(255, 56, 96, 0.8);
            animation: shake 0.5s ease-in-out infinite;
        }

        /* 支付链接样式 */
        .payment-link-container {
            background: linear-gradient(45deg, rgba(198,167,85,0.1), rgba(212,175,55,0.15));
            padding: 25px;
            border-radius: 18px;
            margin: 25px auto;
            max-width: 600px;
            border: 1px solid rgba(198,167,85,0.3);
            transition: var(--transition);
            position: relative;
            overflow: hidden;
        }
        
        .payment-link-container::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(400px circle at var(--mouse-x) var(--mouse-y), 
                        rgba(212, 175, 55, 0.15), transparent 70%);
            z-index: 1;
            opacity: 0;
            transition: opacity 0.4s ease;
        }
        
        .payment-link-container:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.3);
        }
        
        .payment-link-container:hover::before {
            opacity: 1;
        }
        
        .copy-btn {
            padding: 15px 35px;
            background: linear-gradient(90deg, var(--gold-1), var(--gold-2));
            color: var(--black-1);
            border: none;
            border-radius: 50px;
            font-weight: 600;
            font-size: 19px;
            cursor: pointer;
            transition: var(--transition);
            display: block;
            margin: 15px auto 0;
            box-shadow: 0 8px 25px rgba(198,167,85,0.4);
            position: relative;
            z-index: 2;
        }
        
        .copy-btn::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, var(--gold-2), var(--gold-1));
            opacity: 0;
            transition: opacity 0.4s ease;
            z-index: -1;
        }
        
        .copy-btn:hover {
            transform: translateY(-8px) scale(1.05);
            box-shadow: 0 15px 35px rgba(198,167,85,0.6);
        }
        
        .copy-btn:hover::before {
            opacity: 1;
        }
        
        /* 绿色发光按钮 */
        .glow-green-btn {
            background: linear-gradient(90deg, #4CAF50, #8BC34A);
            box-shadow: 0 0 15px rgba(76, 175, 80, 0.6);
            padding: 15px 30px;
            border: none;
            border-radius: 50px;
            font-weight: 600;
            font-size: 18px;
            cursor: pointer;
            transition: var(--transition);
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            color: #fff;
            margin-top: 20px;
            position: relative;
            z-index: 2;
        }
        
        .glow-green-btn::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, #8BC34A, #4CAF50);
            opacity: 0;
            transition: opacity 0.4s ease;
            z-index: -1;
        }
        
        .glow-green-btn:hover {
            transform: translateY(-8px) scale(1.05);
            box-shadow: 0 0 25px rgba(76, 175, 80, 0.8);
        }
        
        .glow-green-btn:hover::before {
            opacity: 1;
        }
        
        .alipay-instructions {
            background: rgba(20,20,20,0.5);
            border: 1px solid rgba(198,167,85,0.3);
            border-radius: 18px;
            padding: 25px;
            margin: 30px auto;
            max-width: 600px;
            transition: var(--transition);
            position: relative;
            overflow: hidden;
        }
        
        .alipay-instructions::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(400px circle at var(--mouse-x) var(--mouse-y), 
                        rgba(212, 175, 55, 0.1), transparent 70%);
            z-index: 1;
            opacity: 0;
            transition: opacity 0.4s ease;
        }
        
        .alipay-instructions:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.3);
        }
        
        .alipay-instructions:hover::before {
            opacity: 1;
        }
        
        .alipay-instructions h3 {
            color: var(--gold-2);
            text-align: center;
            margin-bottom: 20px;
            transition: var(--transition);
            position: relative;
            z-index: 2;
        }
        
        .alipay-instructions:hover h3 {
            color: var(--gold-3);
            text-shadow: 0 0 8px rgba(212, 175, 55, 0.4);
        }
        
        .alipay-steps {
            display: flex;
            flex-direction: column;
            gap: 15px;
            margin-bottom: 25px;
        }
        
        .alipay-step {
            display: flex;
            align-items: flex-start;
            gap: 10px;
            transition: var(--transition);
            padding: 10px;
            border-radius: 8px;
            background: rgba(30, 30, 30, 0.3);
        }
        
        .alipay-step:hover {
            background: rgba(212, 175, 55, 0.1);
            transform: translateX(5px);
        }
        
        .alipay-step i {
            color: var(--gold-2);
            font-size: 20px;
            margin-top: 4px;
            transition: var(--transition);
        }
        
        .alipay-step:hover i {
            transform: scale(1.3);
            color: var(--gold-3);
        }
        
        .alipay-step p {
            color: var(--gold-3);
            margin: 0;
            flex: 1;
            transition: var(--transition);
        }
        
        .alipay-step:hover p {
            color: var(--gold-2);
        }
        
        .get-email-btn {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            width: 100%;
            max-width: 300px;
            margin: 0 auto;
            padding: 15px;
            background: linear-gradient(90deg, var(--gold-1), var(--gold-2));
            color: var(--black-1);
            border: none;
            border-radius: 50px;
            font-weight: 600;
            font-size: 18px;
            cursor: pointer;
            transition: var(--transition);
            position: relative;
            z-index: 2;
        }
        
        .get-email-btn::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, var(--gold-2), var(--gold-1));
            opacity: 0;
            transition: opacity 0.4s ease;
            z-index: -1;
        }
        
        .get-email-btn:hover {
            transform: translateY(-8px) scale(1.05);
            box-shadow: 0 15px 35px rgba(198,167,85,0.6);
        }
        
        .get-email-btn:hover::before {
            opacity: 1;
        }

        /* 邮箱地址样式 */
        .email-display {
            font-size: 24px;
            letter-spacing: 1px;
            font-weight: 600;
            color: var(--gold-3);
            transition: var(--transition);
            padding: 10px;
            border-radius: 8px;
        }
        
        .email-display:hover {
            color: var(--gold-2);
            background: rgba(10, 10, 10, 0.5);
            text-shadow: 0 0 10px rgba(212, 175, 55, 0.4);
            transform: scale(1.03);
        }

        /* 动画 */
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(40px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        @keyframes slideDown {
            from { opacity: 0; transform: translateY(-50px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        @keyframes fadeInUp {
            from { opacity: 0; transform: translateY(80px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        @keyframes scaleIn {
            from { opacity: 0; transform: scale(0.8); }
            to { opacity: 1; transform: scale(1); }
        }

        @keyframes twinkle {
            0% { opacity: 0; transform: scale(0.5); }
            50% { opacity: 0.8; transform: scale(1); }
            100% { opacity: 0; transform: scale(0.5); }
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }
        
        @keyframes float {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-15px); }
            100% { transform: translateY(0px); }
        }
        
        @keyframes pulseError {
            0% { box-shadow: 0 0 5px rgba(255, 56, 96, 0.5); }
            50% { box-shadow: 0 0 20px rgba(255, 56, 96, 0.8); }
            100% { box-shadow: 0 0 5px rgba(255, 56, 96, 0.5); }
        }
        
        @keyframes pulseGreen {
            0% { box-shadow: 0 0 5px rgba(76, 175, 80, 0.5); }
            50% { box-shadow: 0 0 20px rgba(76, 175, 80, 0.8); }
            100% { box-shadow: 0 0 5px rgba(76, 175, 80, 0.5); }
        }
        
        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            75% { transform: translateX(5px); }
        }

        /* 响应式设计 */
        @media (max-width: 768px) {
            .hero h1 {
                font-size: 42px;
            }
            
            .service-card {
                padding: 35px 25px;
            }
            
            .service-icon {
                width: 80px;
                height: 80px;
                font-size: 35px;
            }
            
            .card {
                padding: 35px 25px;
            }
            
            .payment-options {
                gap: 20px;
            }
            
            .payment-option {
                width: 140px;
                padding: 25px 15px;
            }
            
            .birthday-title {
                font-size: 38px;
            }
            
            .gift-icon {
                font-size: 70px;
            }
            
            .passport-title {
                font-size: 36px;
            }
            
            .passport-icon {
                font-size: 80px;
            }
            
            .email-display {
                font-size: 20px;
            }
            
            .radio-group {
                flex-direction: column;
                gap: 15px;
            }
        }
    </style>
</head>
<body>
    <!-- 高级粒子背景 -->
    <div class="particle-layer" id="particles"></div>
    <div class="light-beam"></div>
    
    <!-- 返回按钮 -->
    <div class="back-btn" id="backBtn">
        <i class="fas fa-arrow-left"></i>
    </div>

    <!-- 页面1：主页面 -->
    <div class="page active" id="page1">
        <div class="header">
            <div class="logo">TL SERVICE CENTER</div>
        </div>
        
        <div class="hero">
            <h1>WELCOME</h1>
        </div>
        
        <div class="services-container">
            <div class="service-card" id="purchaseBtn">
                <div class="service-icon">
                    <i class="fas fa-gem"></i>
                </div>
                <h3>产品</h3>
                <p>探索精选</p>
            </div>
            
            <div class="service-card" id="serviceBtn">
                <div class="service-icon">
                    <i class="fas fa-star"></i>
                </div>
                <h3>服务</h3>
                <p>专属服务</p>
            </div>
            
            <div class="service-card" id="contactBtn">
                <div class="service-icon">
                    <i class="fas fa-comments"></i>
                </div>
                <h3>帮助</h3>
                <p>得到Tingling的帮助</p>
            </div>
        </div>
    </div>

    <!-- 页面2：服务页面 -->
    <div class="page" id="page2">
        <div class="card">
            <div class="card-title">
                <h2>你生日？Tingling请客Starbucks</h2>
            </div>
            <div class="form-group">
                <label for="name">您的姓名</label>
                <input type="text" id="name" class="form-control" placeholder="请输入您的姓名">
            </div>
            <div class="form-group">
                <label for="birthday">您的生日</label>
                <input type="date" id="birthday" class="form-control">
            </div>
            <div class="form-group">
                <label>您与Tingling的关系</label>
                <select id="relationship" class="form-control">
                    <option value="">请选择关系</option>
                    <option value="classmate">同学</option>
                    <option value="netfriend">网友</option>
                    <option value="other">其他</option>
                </select>
            </div>
            <div class="form-group" id="otherRelationshipGroup" style="display: none;">
                <label for="otherRelationship">请写明关系</label>
                <input type="text" id="otherRelationship" class="form-control" placeholder="请说明您与Tingling的关系">
            </div>
            <div class="form-group">
                <label for="inviteCode">邀请码</label>
                <input type="text" id="inviteCode" class="form-control" placeholder="请输入邀请码">
            </div>
            <div id="serviceError" class="error-message" style="display: none;">
                <i class="fas fa-exclamation-triangle"></i>
                <span>邀请码错误，请重新输入</span>
            </div>
            <button class="btn" id="submitServiceBtn">提交信息</button>
        </div>
    </div>

    <!-- 页面3：生日祝贺页面 -->
    <div class="page" id="page3">
        <div class="card">
            <div class="birthday-card">
                <div class="birthday-title">你生日？Tingling请客Starbucks</div>
                <div class="gift-icon">
                    <i class="fas fa-gift"></i>
                </div>
                
                <div class="voucher-code">
                    <div class="voucher-title">赠予您的支付宝口令红包</div>
                    <div class="code-display">qmnsxxhs3377</div>
                </div>
                
                <div class="quote">
                    感谢您成为Tingling生命中的一部分
                </div>
            </div>
        </div>
    </div>

    <!-- 页面4：购买页面 -->
    <div class="page" id="page4">
        <div class="card">
            <div class="card-title">
                <h2>产品购买</h2>
            </div>
            <div class="form-group">
                <label for="purchaseName">姓名</label>
                <input type="text" id="purchaseName" class="form-control" placeholder="请输入您的姓名">
            </div>
            
            <div class="form-group">
                <label>性别</label>
                <div class="radio-group">
                    <div class="radio-option">
                        <input type="radio" id="genderMale" name="gender" value="male">
                        <label for="genderMale">男</label>
                    </div>
                    <div class="radio-option">
                        <input type="radio" id="genderFemale" name="gender" value="female">
                        <label for="genderFemale">女</label>
                    </div>
                    <div class="radio-option">
                        <input type="radio" id="genderOther" name="gender" value="other">
                        <label for="genderOther">其他</label>
                    </div>
                </div>
            </div>
            
            <div class="form-group">
                <label for="contactInfo">联系方式</label>
                <input type="text" id="contactInfo" class="form-control" placeholder="请输入电话或邮箱">
            </div>
            
            <div class="form-group">
                <label>是否认识Tingling</label>
                <div class="radio-group">
                    <div class="radio-option">
                        <input type="radio" id="knowYes" name="knowTingling" value="yes">
                        <label for="knowYes">我认识</label>
                    </div>
                    <div class="radio-option">
                        <input type="radio" id="knowNo" name="knowTingling" value="no">
                        <label for="knowNo">不认识</label>
                    </div>
                </div>
            </div>
            
            <div class="form-group">
                <div style="display: flex; align-items: center; gap: 15px; padding: 15px; background: rgba(30,30,30,0.5); border-radius: 12px;">
                    <input type="checkbox" id="voluntaryCheck" style="width: 25px; height: 25px;">
                    <label for="voluntaryCheck" style="margin: 0; font-size: 18px; color: var(--light-gold);">
                        我已年满18周岁
                    </label>
                </div>
            </div>
            
            <div id="purchaseError" class="error-message" style="display: none;">
                <i class="fas fa-exclamation-triangle"></i>
                <span>请完整填写所有信息</span>
            </div>
            
            <button class="btn" id="submitPurchaseBtn">提交购买信息</button>
        </div>
    </div>

    <!-- 页面5：支付页面 -->
    <div class="page" id="page5">
        <div class="card">
            <div class="card-title">
                <h2>支付方式</h2>
            </div>
            <div class="payment-options">
                <div class="payment-option">
                    <i class="fab fa-alipay"></i>
                    <p>支付宝</p>
                </div>
                <div class="payment-option">
                    <i class="fab fa-weixin"></i>
                    <p>微信支付</p>
                </div>
            </div>
            
            <!-- 微信支付区域 - 只显示复制按钮 -->
            <div class="payment-link-container">
                <h3 style="color: var(--gold-2); text-align: center; margin-bottom: 20px;">微信支付</h3>
                <p style="color: var(--gold-3); text-align: center; margin-bottom: 20px;">
                    请点击下方按钮复制支付链接，然后粘贴到微信任意对话框<br>发送后点击打开完成支付
                </p>
                <button class="copy-btn" id="copyWechatPaymentLink">
                    <i class="fas fa-copy"></i> 复制微信支付链接
                </button>
            </div>
            
            <!-- 支付宝支付说明 -->
            <div class="alipay-instructions">
                <h3>支付宝支付</h3>
                <div class="alipay-steps">
                    <div class="alipay-step">
                        <i class="fas fa-1"></i>
                        <p>创建支付宝口令红包</p>
                    </div>
                    <div class="alipay-step">
                        <i class="fas fa-2"></i>
                        <p>设置红包口令</p>
                    </div>
                    <div class="alipay-step">
                        <i class="fas fa-3"></i>
                        <p>将红包口令发送至我们的邮箱</p>
                    </div>
                </div>
                <button class="get-email-btn" id="getEmailBtn">
                    <i class="fas fa-envelope"></i> 获取邮箱地址
                </button>
            </div>
            
            <div class="upload-area" id="uploadArea">
                <i class="fas fa-cloud-upload-alt"></i>
                <h4>上传支付凭证</h4>
                <p>点击或拖拽文件到此处上传</p>
                <input type="file" id="paymentProof" style="display: none;">
            </div>
            
            <div class="form-group">
                <label for="orderNumber">或输入订单号或口令编号</label>
                <input type="text" id="orderNumber" class="form-control" placeholder="请输入订单号或口令编号">
            </div>
            
            <div id="verifyStatus" style="text-align: center; margin: 35px 0; display: none;">
                <div style="display: inline-flex; align-items: center; background: rgba(26, 26, 26, 0.8); 
                    padding: 15px 30px; border-radius: 30px; border: 1px solid var(--gold-2);">
                    <i class="fas fa-check-circle" style="color: var(--gold-2); font-size: 28px; margin-right: 12px;"></i>
                    <span style="color: var(--light-gold); font-size: 18px;">凭证验证成功！</span>
                </div>
            </div>
            
            <button class="btn" id="submitPaymentBtn" style="display: none;">生成通行证</button>
        </div>
    </div>

    <!-- 页面6：问题选择页面 -->
    <div class="page" id="page6">
        <div class="card">
            <div class="card-title">
                <h2>联系Tingling</h2>
            </div>
            <p style="text-align: center; font-size: 20px; color: var(--gold-3); margin-bottom: 40px; max-width: 700px; margin-left: auto; margin-right: auto;">
                请选择您遇到的问题类型，我们将为您提供最有效的解决方案
            </p>
            
            <div class="issues-container">
                <div class="issue-card" data-issue="product">
                    <i class="fas fa-box-open"></i>
                    <h4>产品问题</h4>
                    <p>产品咨询、质量问题、使用问题等</p>
                </div>
                
                <div class="issue-card" data-issue="order">
                    <i class="fas fa-shopping-cart"></i>
                    <h4>订单问题</h4>
                    <p>订单状态、支付问题、物流查询等</p>
                </div>
                
                <div class="issue-card" data-issue="service">
                    <i class="fas fa-headset"></i>
                    <h4>服务问题</h4>
                    <p>会员服务、售后服务、服务咨询等</p>
                </div>
                
                <div class="issue-card" data-issue="other">
                    <i class="fas fa-question-circle"></i>
                    <h4>其他问题</h4>
                    <p>合作咨询、建议反馈、其他问题等</p>
                </div>
            </div>
            
            <button class="btn" id="contactNextBtn">下一步</button>
        </div>
    </div>

    <!-- 页面7：邮箱页面 -->
    <div class="page" id="page7">
        <div class="card">
            <div class="card-title">
                <h2>联系Tingling</h2>
            </div>
            <div style="text-align: center; padding: 40px 0 60px;">
                <div style="font-size: 100px; color: var(--gold-2); margin-bottom: 40px; text-shadow: var(--glow); animation: pulse 3s infinite, float 4s ease-in-out infinite;">
                    <i class="fas fa-envelope-open"></i>
                </div>
                <h3 style="font-size: 28px; color: var(--gold-3); margin-bottom: 30px;">Tingling的邮箱</h3>
                <div style="background: linear-gradient(90deg, rgba(198,167,85,0.12), rgba(212,175,55,0.18)); 
                    padding: 25px; border-radius: 18px; display: inline-block; margin-bottom: 50px;
                    border: 1px solid rgba(198,167,85,0.3); transition: var(--transition);">
                    <p class="email-display">
                        Tingling0702@163.com
                    </p>
                </div>
                
                <!-- 新增绿色发光复制按钮 -->
                <button class="glow-green-btn" id="copyEmailBtn">
                    <i class="fas fa-copy"></i> 复制邮箱地址
                </button>
                
                <p style="font-size: 24px; line-height: 1.8; max-width: 700px; margin: 30px auto 0; color: var(--gold-3); text-shadow: 0 0 15px rgba(212, 175, 55, 0.5);">
                    Tingling欢迎您的到来，我们将尽快回复您的邮件
                </p>
            </div>
        </div>
    </div>

    <!-- 页面8：通行证页面 -->
    <div class="page" id="page8">
        <div class="card">
            <div class="passport-card">
                <div class="passport-title">Welcome</div>
                <div class="passport-icon">
                    <i class="fas fa-id-card"></i>
                </div>
                
                <div class="passport-details">
                    <div class="passport-row">
                        <div class="passport-label">姓名：</div>
                        <div class="passport-value" id="passportName">-</div>
                    </div>
                    <div class="passport-row">
                        <div class="passport-label">性别：</div>
                        <div class="passport-value" id="passportGender">-</div>
                    </div>
                    <div class="passport-row">
                        <div class="passport-label">认识Tingling：</div>
                        <div class="passport-value" id="passportKnowTingling">-</div>
                    </div>
                    <div class="passport-row">
                        <div class="passport-label">联系方式：</div>
                        <div class="passport-value" id="passportContact">-</div>
                    </div>
                    <div class="passport-row">
                        <div class="passport-label">通行证号：</div>
                        <div class="passport-value" id="passportNumber">-</div>
                    </div>
                </div>
                
                <div class="passport-code" id="passportCode">TL-20250702-3377</div>
                
                <p style="font-size: 18px; color: var(--gold-3); max-width: 600px; margin: 30px auto; line-height: 1.8; text-align: center;">
                    This service is furnished by TL.
                </p>
            </div>
        </div>
    </div>

    <!-- 服务码验证模态框 -->
    <div class="modal" id="serviceModal">
        <div class="modal-content">
            <span class="close-modal" id="closeServiceModal">&times;</span>
            <div class="modal-title">服务验证</div>
            <div class="form-group">
                <label for="serviceCode">请输入服务码</label>
                <input type="password" id="serviceCode" class="form-control" placeholder="请输入6位服务码">
            </div>
            <div id="serviceError" class="error-message" style="display: none;">
                <i class="fas fa-exclamation-triangle"></i>
                <span>您暂未拥有进入服务资格</span>
            </div>
            <button class="btn" id="verifyServiceBtn">验证并进入</button>
        </div>
    </div>

    <!-- 管理员界面 -->
    <div class="modal" id="adminPanel">
        <div class="modal-content">
            <span class="close-modal" id="closeAdminPanel">&times;</span>
            <div class="modal-title">管理员控制面板</div>
            
            <div style="display: flex; justify-content: space-between; margin-bottom: 40px;">
                <button class="btn" id="adminBackBtn" style="width: auto; padding: 12px 25px; background: linear-gradient(90deg, var(--gold-1), var(--gold-2));">
                    <i class="fas fa-arrow-left"></i> 返回
                </button>
                <button class="btn" id="saveSettingsBtn" style="width: auto; margin: 0; padding: 12px 30px; background: linear-gradient(90deg, var(--gold-1), var(--gold-2));">
                    <i class="fas fa-save"></i> 保存设置
                </button>
            </div>
            
            <div class="card" style="margin-bottom: 30px;">
                <div class="card-content">
                    <h3 style="color: var(--gold-2); margin-bottom: 30px; font-size: 24px;">
                        <i class="fas fa-cog"></i> 系统设置
                    </h3>
                    <div class="form-group">
                        <label for="adminServiceCode">服务码</label>
                        <input type="text" id="adminServiceCode" class="form-control" value="337737">
                    </div>
                    <div class="form-group">
                        <label for="adminInviteCode">邀请码</label>
                        <input type="text" id="adminInviteCode" class="form-control" value="20250702">
                    </div>
                    <div class="form-group">
                        <label for="adminPassword">管理员密码</label>
                        <input type="password" id="adminPassword" class="form-control" value="xgsafj3377">
                    </div>
                </div>
            </div>
            
            <div class="card">
                <div class="card-content">
                    <h3 style="color: var(--gold-2); margin-bottom: 30px; font-size: 24px;">
                        <i class="fas fa-credit-card"></i> 支付设置
                    </h3>
                    <div class="form-group">
                        <label for="paymentImage">支付二维码</label>
                        <input type="file" id="paymentImage" class="form-control">
                    </div>
                    <div class="form-group">
                        <label for="paymentLink">支付链接</label>
                        <input type="text" id="paymentLink" class="form-control" placeholder="请输入支付链接">
                    </div>
                    <div class="form-group">
                        <label for="paymentMessage">支付说明</label>
                        <textarea id="paymentMessage" class="form-control" rows="4" placeholder="请输入支付说明"></textarea>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // 存储设置
        let settings = {
            serviceCode: '337737',
            inviteCode: '20250702',
            adminPassword: 'xgsafj3377'
        };
        
        // 从本地存储加载设置
        function loadSettings() {
            const savedSettings = localStorage.getItem('tlSettings');
            if (savedSettings) {
                settings = JSON.parse(savedSettings);
                
                // 更新管理界面输入框
                document.getElementById('adminServiceCode').value = settings.serviceCode;
                document.getElementById('adminInviteCode').value = settings.inviteCode;
                document.getElementById('adminPassword').value = settings.adminPassword;
            }
        }
        
        // 保存设置
        function saveSettings() {
            settings.serviceCode = document.getElementById('adminServiceCode').value;
            settings.inviteCode = document.getElementById('adminInviteCode').value;
            settings.adminPassword = document.getElementById('adminPassword').value;
            
            localStorage.setItem('tlSettings', JSON.stringify(settings));
        }
        
        // 生成高级粒子背景
        function createParticles() {
            const container = document.getElementById('particles');
            const particleCount = 150;
            const types = ['circle', 'triangle', 'square'];
            
            for (let i = 0; i < particleCount; i++) {
                const particle = document.createElement('div');
                particle.classList.add('gold-particle');
                
                // 随机形状
                const shape = types[Math.floor(Math.random() * types.length)];
                if (shape === 'triangle') {
                    particle.style.borderRadius = '0';
                    particle.style.clipPath = 'polygon(50% 0%, 0% 100%, 100% 100%)';
                    particle.style.backgroundColor = 'transparent';
                    particle.style.border = 'solid transparent';
                    particle.style.borderWidth = '0 5px 10px 5px';
                    particle.style.borderBottomColor = `rgba(212, 175, 55, ${0.3 + Math.random() * 0.4})`;
                } else if (shape === 'square') {
                    particle.style.borderRadius = '4px';
                }
                
                // 随机位置
                const posX = Math.random() * 100;
                const posY = Math.random() * 100;
                particle.style.left = `${posX}%`;
                particle.style.top = `${posY}%`;
                
                // 随机大小
                const size = 5 + Math.random() * 15;
                particle.style.width = `${size}px`;
                particle.style.height = shape === 'triangle' ? '0' : `${size}px`;
                
                // 随机动画延迟和时长
                const delay = Math.random() * 5;
                const duration = 3 + Math.random() * 4;
                particle.style.animationDelay = `${delay}s`;
                particle.style.animationDuration = `${duration}s`;
                
                // 随机颜色
                const golds = ['#d4af37', '#c6a755', '#e6d6a9'];
                const color = golds[Math.floor(Math.random() * golds.length)];
                if (shape !== 'triangle') {
                    particle.style.backgroundColor = color;
                }
                
                container.appendChild(particle);
            }
        }
        
        // 页面切换函数
        function showPage(pageId) {
            document.querySelectorAll('.page').forEach(page => {
                page.classList.remove('active');
            });
            document.getElementById(pageId).classList.add('active');
        }

        // 返回按钮
        document.getElementById('backBtn').addEventListener('click', function() {
            showPage('page1');
        });

        // 服务卡片点击事件
        document.getElementById('serviceBtn').addEventListener('click', function() {
            document.getElementById('serviceModal').style.display = 'flex';
        });

        // 关闭服务模态框
        document.getElementById('closeServiceModal').addEventListener('click', function() {
            document.getElementById('serviceModal').style.display = 'none';
        });

        // 验证服务码 - 进入不同页面
        document.getElementById('verifyServiceBtn').addEventListener('click', function() {
            const serviceCode = document.getElementById('serviceCode').value;
            const errorElement = document.getElementById('serviceError');
            
            if(serviceCode === settings.serviceCode) {
                document.getElementById('serviceModal').style.display = 'none';
                showPage('page2');
            } else if(serviceCode === settings.adminPassword) {
                document.getElementById('serviceModal').style.display = 'none';
                document.getElementById('adminPanel').style.display = 'flex';
            } else {
                errorElement.style.display = 'flex';
                setTimeout(() => {
                    errorElement.style.display = 'none';
                }, 3000);
            }
        });

        // 关系选择事件
        document.getElementById('relationship').addEventListener('change', function() {
            const otherGroup = document.getElementById('otherRelationshipGroup');
            if(this.value === 'other') {
                otherGroup.style.display = 'block';
            } else {
                otherGroup.style.display = 'none';
            }
        });

        // 提交服务信息
        document.getElementById('submitServiceBtn').addEventListener('click', function() {
            const inviteCode = document.getElementById('inviteCode').value;
            const errorElement = document.getElementById('serviceError');
            
            if(inviteCode === settings.inviteCode) {
                showPage('page3');
            } else {
                errorElement.style.display = 'flex';
                setTimeout(() => {
                    errorElement.style.display = 'none';
                }, 3000);
            }
        });

        // 购买按钮
        document.getElementById('purchaseBtn').addEventListener('click', function() {
            showPage('page4');
        });

        // 提交购买信息
        document.getElementById('submitPurchaseBtn').addEventListener('click', function() {
            const name = document.getElementById('purchaseName').value;
            const contact = document.getElementById('contactInfo').value;
            const gender = document.querySelector('input[name="gender"]:checked');
            const knowTingling = document.querySelector('input[name="knowTingling"]:checked');
            const voluntaryCheck = document.getElementById('voluntaryCheck').checked;
            const errorElement = document.getElementById('purchaseError');
            
            // 检查所有必填项
            if(!name || !contact || !gender || !knowTingling || !voluntaryCheck) {
                errorElement.style.display = 'flex';
                setTimeout(() => {
                    errorElement.style.display = 'none';
                }, 3000);
                return;
            }
            
            // 所有信息完整，继续下一步
            showPage('page5');
        });

        // 联系按钮
        document.getElementById('contactBtn').addEventListener('click', function() {
            showPage('page6');
        });

        // 问题选择下一步
        document.getElementById('contactNextBtn').addEventListener('click', function() {
            showPage('page7');
        });

        // 凭证上传区域点击事件
        document.getElementById('uploadArea').addEventListener('click', function() {
            document.getElementById('paymentProof').click();
        });

        // 支付凭证上传处理
        document.getElementById('paymentProof').addEventListener('change', function(e) {
            if(e.target.files.length > 0) {
                document.getElementById('verifyStatus').style.display = 'block';
                document.getElementById('submitPaymentBtn').style.display = 'block';
            }
        });

        // 订单号输入处理
        document.getElementById('orderNumber').addEventListener('input', function() {
            if(this.value.length > 5) {
                document.getElementById('verifyStatus').style.display = 'block';
                document.getElementById('submitPaymentBtn').style.display = 'block';
            } else {
                document.getElementById('verifyStatus').style.display = 'none';
                document.getElementById('submitPaymentBtn').style.display = 'none';
            }
        });

        // 关闭管理员面板
        document.getElementById('closeAdminPanel').addEventListener('click', function() {
            document.getElementById('adminPanel').style.display = 'none';
        });

        // 管理员面板返回按钮
        document.getElementById('adminBackBtn').addEventListener('click', function() {
            document.getElementById('adminPanel').style.display = 'none';
        });

        // 保存设置
        document.getElementById('saveSettingsBtn').addEventListener('click', function() {
            saveSettings();
            
            // 创建保存成功动画
            const saveBtn = document.getElementById('saveSettingsBtn');
            const originalText = saveBtn.innerHTML;
            
            saveBtn.innerHTML = '<i class="fas fa-check"></i> 设置已保存';
            saveBtn.style.background = 'linear-gradient(90deg, #4CAF50, #8BC34A)';
            
            setTimeout(() => {
                saveBtn.innerHTML = originalText;
                saveBtn.style.background = 'linear-gradient(90deg, var(--gold-1), var(--gold-2))';
            }, 2000);
        });
        
        // 生成通行证
        document.getElementById('submitPaymentBtn').addEventListener('click', function() {
            const name = document.getElementById('purchaseName').value || '尊贵客户';
            const contact = document.getElementById('contactInfo').value || '未提供';
            
            // 获取性别
            const gender = document.querySelector('input[name="gender"]:checked');
            const genderText = gender ? (gender.value === 'male' ? '男' : 
                                       gender.value === 'female' ? '女' : '其他') : '未选择';
            
            // 获取是否认识Tingling
            const knowTingling = document.querySelector('input[name="knowTingling"]:checked');
            const knowText = knowTingling ? (knowTingling.value === 'yes' ? '我认识' : '不认识') : '未选择';
            
            // 设置通行证信息
            document.getElementById('passportName').textContent = name;
            document.getElementById('passportGender').textContent = genderText;
            document.getElementById('passportKnowTingling').textContent = knowText;
            document.getElementById('passportContact').textContent = contact;
            
            // 生成当前日期时间格式的通行证号 (TL+年月日时分)
            const now = new Date();
            const year = now.getFullYear();
            const month = String(now.getMonth() + 1).padStart(2, '0');
            const day = String(now.getDate()).padStart(2, '0');
            const hours = String(now.getHours()).padStart(2, '0');
            const minutes = String(now.getMinutes()).padStart(2, '0');
            
            const passportNum = `TL${year}${month}${day}${hours}${minutes}`;
            document.getElementById('passportNumber').textContent = passportNum;
            
            // 通行证代码
            document.getElementById('passportCode').textContent = passportNum;
            
            // 显示通行证页面
            showPage('page8');
        });
        
        // 复制微信支付链接
        document.getElementById('copyWechatPaymentLink').addEventListener('click', function() {
            const paymentLink = '#付款:Tinglingo(xgsafj3377)/收款/001';
            navigator.clipboard.writeText(paymentLink).then(() => {
                // 提示复制成功
                const btn = document.getElementById('copyWechatPaymentLink');
                const originalText = btn.innerHTML;
                btn.innerHTML = '<i class="fas fa-check"></i> 已复制到剪贴板';
                setTimeout(() => {
                    btn.innerHTML = originalText;
                }, 2000);
            }).catch(err => {
                console.error('复制失败:', err);
                alert('复制失败，请手动复制');
            });
        });
        
        // 获取邮箱按钮
        document.getElementById('getEmailBtn').addEventListener('click', function() {
            showPage('page7');
        });
        
        // 复制邮箱地址
        document.getElementById('copyEmailBtn').addEventListener('click', function() {
            const email = 'Tingling0702@163.com';
            navigator.clipboard.writeText(email).then(() => {
                // 提示复制成功
                const btn = document.getElementById('copyEmailBtn');
                const originalText = btn.innerHTML;
                btn.innerHTML = '<i class="fas fa-check"></i> 邮箱已复制';
                setTimeout(() => {
                    btn.innerHTML = originalText;
                }, 2000);
            }).catch(err => {
                console.error('复制失败:', err);
                alert('复制失败，请手动复制');
            });
        });
        
        // 添加鼠标跟随光效
        document.addEventListener('mousemove', function(e) {
            document.documentElement.style.setProperty('--mouse-x', `${e.clientX}px`);
            document.documentElement.style.setProperty('--mouse-y', `${e.clientY}px`);
        });

        // 初始化设置
        loadSettings();
        
        // 初始化粒子背景
        window.addEventListener('DOMContentLoaded', createParticles);
        
        // 关闭所有模态框（点击背景）
        document.querySelectorAll('.modal').forEach(modal => {
            modal.addEventListener('click', function(e) {
                if (e.target === this) {
                    this.style.display = 'none';
                }
            });
        });
    </script>
</body>
</html>
