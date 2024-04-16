# Passwordgenerator
Der Benutzer kann die Länge des generierten Passworts festlegen und dann auf eine Schaltfläche klicken, um ein zufälliges Passwort zu generieren. Das generierte Passwort wird dann auf der Webseite angezeigt. Das Projekt verwendet nur PHP und HTML und erfordert keine Datenbank.
<?php
// Funktion zum Generieren eines zufälligen Passworts
function generatePassword($length = 10) {
    $characters = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!@#$%^&*()-_';
    $password = '';
    $character_length = strlen($characters);
    for ($i = 0; $i < $length; $i++) {
        $password .= $characters[rand(0, $character_length - 1)];
    }
    return $password;
}

// Standardlänge des Passworts
$password_length = 12;

// Wenn das Formular abgesendet wurde, das Passwort generieren
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    if(isset($_POST['length']) && is_numeric($_POST['length'])) {
        $password_length = $_POST['length'];
    }
    $generated_password = generatePassword($password_length);
}
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Password Generator</title>
</head>
<body>
    <h1>Password Generator</h1>
    <form method="post">
        <label for="length">Password Length (default: <?php echo $password_length; ?>):</label><br>
        <input type="number" id="length" name="length" min="6" max="20" value="<?php echo $password_length; ?>"><br><br>
        <button type="submit">Generate Password</button>
    </form>
    <?php if(isset($generated_password)): ?>
        <h2>Generated Password:</h2>
        <p><?php echo $generated_password; ?></p>
    <?php endif; ?>
</body>
</html>
