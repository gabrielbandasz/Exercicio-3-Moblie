# Exercício 3 - Mobile

# Pedra, Papel e Tesoura

## MainActivity.java

```java
package br.ulbra.pedrapapeltesoura;

import android.os.Bundle;
import android.view.View;
import android.widget.ImageView;
import android.widget.TextView;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;

import java.util.Random;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        EdgeToEdge.enable(this);
        setContentView(R.layout.activity_main);

        ViewCompat.setOnApplyWindowInsetsListener(
                findViewById(R.id.main),
                (v, insets) -> {
                    Insets systemBars = insets.getInsets(
                            WindowInsetsCompat.Type.systemBars()
                    );

                    v.setPadding(
                            systemBars.left,
                            systemBars.top,
                            systemBars.right,
                            systemBars.bottom
                    );

                    return insets;
                }
        );
    }

    public void selecionarPedra(View view) {
        verificarGanhador("pedra");
    }

    public void selecionarPapel(View view) {
        verificarGanhador("papel");
    }

    public void selecionarTesoura(View view) {
        verificarGanhador("tesoura");
    }

    private String gerarEscolhaAleatoriaApp() {

        String[] opcoes = {"pedra", "papel", "tesoura"};

        int numeroAleatorio = new Random().nextInt(3);

        ImageView imagemApp = findViewById(R.id.imageView);

        String escolhaApp = opcoes[numeroAleatorio];

        switch (escolhaApp) {

            case "pedra":
                imagemApp.setImageResource(R.drawable.pedra);
                break;

            case "papel":
                imagemApp.setImageResource(R.drawable.papel);
                break;

            case "tesoura":
                imagemApp.setImageResource(R.drawable.tesoura);
                break;
        }

        return escolhaApp;
    }

    private void verificarGanhador(String escolhaUsuario) {

        String escolhaApp = gerarEscolhaAleatoriaApp();

        TextView textoResultado = findViewById(R.id.textView4);

        if ((escolhaApp.equals("pedra") && escolhaUsuario.equals("tesoura")) ||
                (escolhaApp.equals("papel") && escolhaUsuario.equals("pedra")) ||
                (escolhaApp.equals("tesoura") && escolhaUsuario.equals("papel"))) {

            textoResultado.setText("Você perdeu :(");

        } else if ((escolhaUsuario.equals("pedra") && escolhaApp.equals("tesoura")) ||
                (escolhaUsuario.equals("papel") && escolhaApp.equals("pedra")) ||
                (escolhaUsuario.equals("tesoura") && escolhaApp.equals("papel"))) {

            textoResultado.setText("Você ganhou :)");

        } else {

            textoResultado.setText("Deu empate!!!");
        }
    }
}
```

## activity_main.xml

```xml
<?xml version="1.0" encoding="utf-8"?>

<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/TextView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Pedra Papel"
        android:textSize="34sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <TextView
        android:id="@+id/textView3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="&amp; Tesoura"
        android:textSize="34sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/TextView" />

    <TextView
        android:id="@+id/textView2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="50dp"
        android:text="Escolha do App"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/textView3" />

    <TextView
        android:id="@+id/textView4"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="196dp"
        android:text="Escolha uma opção abaixo"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/textView2" />

    <ImageView
        android:id="@+id/imageView"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:layout_marginTop="20dp"
        app:srcCompat="@drawable/padrao"
        app:layout_constraintTop_toBottomOf="@id/textView2"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent" />

    <ImageView
        android:id="@+id/imageView3"
        android:layout_width="102dp"
        android:layout_height="98dp"
        android:layout_marginTop="20dp"
        android:layout_marginEnd="150dp"
        android:onClick="selecionarPedra"
        app:srcCompat="@drawable/pedra"
        app:layout_constraintTop_toBottomOf="@id/textView4"
        app:layout_constraintEnd_toEndOf="parent" />

    <ImageView
        android:id="@+id/imageView2"
        android:layout_width="96dp"
        android:layout_height="96dp"
        android:layout_marginTop="20dp"
        android:layout_marginStart="25dp"
        android:onClick="selecionarPapel"
        app:srcCompat="@drawable/papel"
        app:layout_constraintTop_toBottomOf="@id/textView4"
        app:layout_constraintStart_toStartOf="parent" />

    <ImageView
        android:id="@+id/imageView4"
        android:layout_width="93dp"
        android:layout_height="97dp"
        android:layout_marginTop="20dp"
        android:layout_marginEnd="25dp"
        android:onClick="selecionarTesoura"
        app:srcCompat="@drawable/tesoura"
        app:layout_constraintTop_toBottomOf="@id/textView4"
        app:layout_constraintEnd_toEndOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```
