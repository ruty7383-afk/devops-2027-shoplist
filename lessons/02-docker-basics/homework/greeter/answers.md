1.docker build -t greeter :v1 lessons/02-docker-basics/homework/greeter/
2. docker run -d --name greeter -p 9000:8000 greeter:v1
3.docker run -d --name greeter -p 9000:8000 -e GREETING=Shalom greeter:v1
4. Shalom , Rivka!
5. השלבים של התקנת התלויות יישארו ב-cache, כי הקובץ requirements.txt לא השתנה.
שלבים כמוו:COPY requirements.txt .
                                       יסומנו כCACHED והשלב שמעתיק ירוץ מחדש               RUN pip install --no-cache-dir -r requirements.txt 
הסיבה היא ש-Docker שומר כל שלב כ-layer. כל עוד הקבצים שמשפיעים על שלב מסוים לא השתנו, Docker יכול להשתמש ב-cache. ברגע ש-app.py השתנה, ה-layer שמעתיק אותו כבר לא זהה ולכן הוא נבנה מחדש.
