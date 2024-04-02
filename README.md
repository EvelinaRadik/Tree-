java
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity implements View.OnClickListener {
    private Button[][] buttons = new Button[3][3];
    private boolean player1Turn = true;
    private int roundCount;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                String buttonID = "button_" + i + j;
                int resID = getResources().getIdentifier(buttonID, "id", getPackageName());
                buttons[i][j] = findViewById(resID);
                buttons[i][j].setOnClickListener(this);
            }
        }

        Button resetButton = findViewById(R.id.button_reset);
        resetButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                resetGame();
            }
        });
    }

    @Override
    public void onClick(View v) {
        if (!((Button)v).getText().toString().equals("")) {
            return;
        }

        if (player1Turn) {
            ((Button)v).setText("X");
        } else {
            ((Button)v).setText("O");
        }

        roundCount++;

        if (checkForWin()) {
            if (player1Turn) {
                player1Wins();
            } else {
                player2Wins();
            }
        } else if (roundCount == 9) {
            draw();
        } else {
            player1Turn = !player1Turn;
        }
    }

    private boolean checkForWin() {
        String[][] field = new String[3][3];

        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                field[i][j] = buttons[i][j].getText().toString();
            }
        }

        for (int i = 0; i < 3; i++) {
            if (field[i][0].equals(field[i][1]) && field[i][0].equals(field[i][2]) && !field[i][0].equals("")) {
                return true;
            }
        }

        for (int i = 0; i < 3; i++) {
            if (field[0][i].equals(field[1][i]) && field[0][i].equals(field[2][i]) && !field[0][i].equals("")) {
                return true;
            }
        }

        if (field[0][0].equals(field[1][1]) && field[0][0].equals(field[2][2]) && !field[0][0].equals("")) {
            return true;
        }

        if (field[0][2].equals(field[1][1]) && field[0][2].equals(field[2][0]) && !field[0][2].equals("")) {
            return true;
        }

        return false;
    }

    private void player1Wins() {
        Toast.makeText(this, "Player 1 wins!", Toast.LENGTH_SHORT).show();
        resetGame();
    }

    private void player2Wins() {
        Toast.makeText(this, "Player 2 wins!", Toast.LENGTH_SHORT).show();
        resetGame();
    }

    private void draw() {
        Toast.makeText(this, "Draw!", Toast.LENGTH_SHORT).show();
        resetGame();
    }

    private void resetGame() {
        player1Turn = true;
        roundCount = 0;

        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                buttons[i][j].setText("");
            }
        }
    }
}


В файле activity_main.xml должно быть следующее содержимое для создания макета:

xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <LinearLayout
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerInParent="true"
        android:orientation="vertical">

        <LinearLayout
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:orientation="horizontal">

            <Button
android:id="@+id/button_00"
                android:layout_width="100dp"
                android:layout_height="100dp"
                android:layout_margin="5dp"
                android:textSize="25sp" />

            <Button
                android:id="@+id/button_01"
                android:layout_width="100dp"
                android:layout_height="100dp"
                android:layout_margin="5dp"
                android:textSize="25sp" />

            <Button
                android:id="@+id/button_02"
                android:layout_width="100dp"
                android:layout_height="100dp"
                android:layout_margin="5dp"
                android:textSize="25sp" />

        </LinearLayout>

        <LinearLayout
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:orientation="horizontal">

            <Button
                android:id="@+id/button_10"
                android:layout_width="100dp"
                android:layout_height="100dp"
                android:layout_margin="5dp"
                android:textSize="25sp" />

            <Button
                android:id="@+id/button_11"
                android:layout_width="100dp"
                android:layout_height="100dp"
                android:layout_margin="5dp"
                android:textSize="25sp" />

            <Button
                android:id="@+id/button_12"
                android:layout_width="100dp"
                android:layout_height="100dp"
                android:layout_margin="5dp"
                android:textSize="25sp" />

        </LinearLayout>

        <LinearLayout
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:orientation="horizontal">

            <Button
                android:id="@+id/button_20"
                android:layout_width="100dp"
                android:layout_height="100dp"
                android:layout_margin="5dp"
                android:textSize="25sp" />

            <Button
                android:id="@+id/button_21"
                android:layout_width="100dp"
                android:layout_height="100dp"
                android:layout_margin="5dp"
                android:textSize="25sp" />

            <Button
                android:id="@+id/button_22"
                android:layout_width="100dp"
                android:layout_height="100dp"
                android:layout_margin="5dp"
                android:textSize="25sp" />

        </LinearLayout>

    </LinearLayout>

    <Button
        android:id="@+id/button_reset"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/button_22"
        android:layout_centerHorizontal="true"
        android:marginTop="20dp"
        android:text="Reset" />

</RelativeLayout>
