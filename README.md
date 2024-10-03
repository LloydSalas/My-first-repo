<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Food Delivery Form</title>
    <script type="module" src="https://cdn.jsdelivr.net/npm/@ionic/core/dist/ionic/ionic.esm.js"></script>
    <script nomodule src="https://cdn.jsdelivr.net/npm/@ionic/core/dist/ionic/ionic.js"></script>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@ionic/core/css/ionic.bundle.css" />
</head>
<body>

<ion-app>

    <!-- Header -->
    <ion-header>
        <ion-toolbar color="tertiary">
            <ion-title>Food Delivery</ion-title>
        </ion-toolbar>
    </ion-header>
    
    <!-- Content -->
    <ion-content class="ion-padding">

        <!-- Monthly Income -->
        <ion-item>
            <ion-input 
            id="name"
            label="Enter your name"
            label-placement="floating"  
            type="text"></ion-input>
        </ion-item>

        <!-- Product Name -->
        <ion-item>
            <ion-input 
            id="product_name"
            label="Enter the product name"
            label-placement="floating"  
            type="text"></ion-input>
        </ion-item>

        <!-- Product Price -->
        <ion-item>
            <ion-input 
            id="product_price"
            label="Enter the product price"
            label-placement="floating"  
            type="number"></ion-input>
        </ion-item>

        <!-- Discount -->
        <ion-list>
            <ion-item>
                <ion-select label="Discount" id="discount" placeholder="Want a discount?" (ionChange)="myChange()">
                    <ion-select-option value="yes">Yes</ion-select-option>
                    <ion-select-option value="no">No</ion-select-option>
                </ion-select>
            </ion-item>
            <ion-item id="notdisplay" style="display: none;">
                <ion-input 
                id="voucher"
                label="Enter the voucher code"
                label-placement="floating"  
                type="text"></ion-input>
            </ion-item>
        </ion-list>

        <br>

        <!-- Button -->
        <ion-button expand="full" onclick="triggerMode()" color="primary">SUBMIT ORDER</ion-button>
        <br>
        
        <!-- Result -->
        <div>
            <ion-card>
                <ion-card-header>
                    <ion-card-title ion-card-title>Display Result</ion-card-title>
                </ion-card-header>
                <ion-card-content id="res">The result will appear here...</ion-card-content>
            </ion-card>
        </div>

    </ion-content>
</ion-app>

<script>
    document.getElementById('discount').addEventListener("ionChange", myChange)
    function myChange(){
        const discount = document.getElementById('discount').value
        const notDisplay = document.getElementById('notdisplay')

        if (discount == "yes"){
            notDisplay.style.display = "block"
        }
    }

    function triggerMode(){
        const name = document.getElementById('name').value
        const product_name = document.getElementById('product_name').value
        const product_price = parseInt(document.getElementById('product_price').value)
        const discount = document.getElementById('discount').value
        const voucher = document.getElementById('voucher').value.toLowerCase()

        let total = product_price;
        let vouch_text = "";
        let output = "";
        
        if (discount == "yes"){
            if (voucher == "christian"){
                total = product_price - (product_price * 0.1)
                vouch_text = voucher
            } else {
                vouch_text = "Invalid Voucher Code!"
            }
        } else if (discount == "no"){
            vouch_text = "No discount!"
        }

        if (discount == "yes" || discount == "no"){
            output = document.getElementById('res').innerHTML = Name: <b>${name}</b><br>Product Name: <b>${product_name}</b><br>Product Price: <b>${product_price}</b><br>Discount Code: <b>${vouch_text}</b><br>Total Cost: <b>${total}</b>
        }
    }
</script>

</body>
</html>

