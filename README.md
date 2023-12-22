import android.content.Context;
import android.graphics.Canvas;
import android.graphics.Paint;
import android.graphics.Point;
import android.view.MotionEvent;
import android.view.View;
import java.util.ArrayList;

public class DotsView extends View {
    private ArrayList<Point> points = new ArrayList<>();
    private Paint paint = new Paint();

    public DotsView(Context context) {
        super(context);
    }

    @Override
    public boolean onTouchEvent(MotionEvent event) {
        if (event.getAction() == MotionEvent.ACTION_DOWN) {
            points.add(new Point((int)event.getX(), (int)event.getY()));
            invalidate(); // force a redraw
            return true;
        }
        return super.onTouchEvent(event);
    }

    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);
        for (Point point : points) {
            canvas.drawCircle(point.x, point.y, 10, paint);
        }
        if (points.size() > 1) {
            for (int i = 0; i < points.size() - 1; i++) {
                Point point1 = points.get(i);
                Point point2 = points.get(i + 1);
                canvas.drawLine(point1.x, point1.y, point2.x, point2.y, paint);
            }
        }
