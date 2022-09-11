<img src="https://github.com/yuliitezary/yuliitezary/blob/main/github-user-contribution.svg" width="1000" height="300"  /></p>
все команды которой я ешё не автоматьзировал
all the commands of which I have not automated yet
```
Запись экрана:
ffmpeg.exe -y -rtbufsize 100M -f gdigrab -framerate 30 -probesize 10M -draw_mouse 1 -i desktop -c:v libx264 -r 30 -preset ultrafast -tune zerolatency -crf 25 -pix_fmt yuv420p screen.mp4
 
Перевод в другой формат, с другими кодеками:
ffmpeg -i out.avi -c:v vp9 -b:v 100K Triangle.mp4
 
Видеомонтаж
ffmpeg -i Tok2.mp4 -lavfi '[0:v]scale=ih*16/9:-1,boxblur=luma_radius=min(h\,w)/20:luma_power=1:chroma_radius=min(cw\,ch)/20:chroma_power=1[bg];[bg][0:v]overlay=(W-w)/2:(H-h)/2,crop=h=iw*9/16' -vb 800K TriangleTok2.mp4
 
Обьединение файлов из списка:
ffmpeg -f concat -safe 0 -i list.txt -c copy OUTTriangle.mp4
 
Прямая тренсляция файла
ffmpeg -i OUTTriangle.mp4 -f flv rtmp://a.rtmp.youtube.com/live2/5wkv-15m3-3zme-zb2u
ffmpeg -i Pes-2.avi -vcodec libx264 -profile:v baseline -b:v 1000k -maxrate 1000k -bufsize 1000k -r 24 -f flv rtmp://a.rtmp.youtube.com/live2/q18p-8mbg-tw50-djr3-5p62
 
Прямая трансляция чужого потока:
ffmpeg -i $(youtube-dl -f best --get-url https://youtu.be/5qap5aO4i9A) -f flv rtmp://a.rtmp.youtube.com/live2/5wkv-15m3-3zme-zb2u

УВЕЛИЧИТЬ/УМЕНЬШИТЬ СКОРОСТЬ ВИДЕО
Чтобы увеличить скорость воспроизведения видео мы будем использовать фильтры, с помощью опции -vf. За скорость отвечает фильтр setpts. Например:

 ffmpeg -i video.mpg -vf "setpts=4*PTS" highspeed.mpg

А так можно уменьшить скорость:

 ffmpeg -i video.mpg -vf "setpts=0.5*PTS" lowerspeed.mpg -hide_banner

ОБРЕЗАТЬ ВИДЕО
Тут уже фильтры нам не помогут, но зато мы можем указать опциями из какого момента нужно начать и где завершить, например:

 ffmpeg -i video.mp4 -ss 00:01:00 -t 00:01:00 -c copy video_clip.mp4

Начинаем от минуты и пишем еще минуту:

-ss задает время на видео, из которого стоит начать запись;
-t задает время когда запись нужно завершить относительно ss;
-с задает кодеки для аудио и видео, в нашем случае просто копировать файлы, ничего не перекодируя.


СКЛЕИТЬ ДВА ВИДЕО
Чтобы склеить два видео используйте команду:

 ffmpeg -i concat:"video1.mpg|video2.mpg" -c copy video.mpg
```
```
скопировать видео начиная с 5 секунды - продолжительностью 15 секунд
ffmpeg -i 1.mp4 -ss 00:00:05 -codec copy -t 00:00:15 out.mp4
--------------------------------------
скопировать 1 минуту 27 секунд - с конца видео
ffmpeg -sseof -00:01:27 -i 1.mp4 -c copy out.mp4
--------------------------------------
конвертировать видео например .flv в .avi  сначала распаковываем в контейнер .ts
ffmpeg -i 1.flv -acodec copy -vcodec copy -vbsf h264_mp4toannexb -f mpegts 11.ts
ffmpeg -i "concat:11.ts" -vcodec copy -acodec copy out.avi
--------------------------------------
склеить 3 видеофайла MP4   сначала распаковываем в контейнер .ts
ffmpeg -i 1.mp4 -acodec copy -vcodec copy -vbsf h264_mp4toannexb -f mpegts 11.ts
ffmpeg -i 2.mp4 -acodec copy -vcodec copy -vbsf h264_mp4toannexb -f mpegts 22.ts
ffmpeg -i 3.mp4 -acodec copy -vcodec copy -vbsf h264_mp4toannexb -f mpegts 33.ts
ffmpeg -i "concat:11.ts|22.ts|33.ts" -vcodec copy -acodec copy out.mp4
--------------------------------------
скопировать с 10 секунды с начала видео
ffmpeg -ss 00:00:10 -i 1.mp4 -c copy out.mp4
--------------------------------------
Разбить видео по кадрам. создаём папку FOTO внутри папки ffmpeg -  ffmpeg\FOTO 
нажимаем клавишу SHIFT - внутри папки ffmpeg, правой клавишей мышки вызываем меню, должно появится "ОТКРЫТЬ ОКНО КОМАНД" - запускаем Командную строку - вставляем команду
ffmpeg -i 1.mp4 FOTO/image%d.png 
жмём ENTR

--------------------------------------
ЗАХВАТ ЭКРАНА
ffmpeg.exe -y -rtbufsize 100M -f gdigrab -framerate 30 -probesize 10M -draw_mouse 1 -i desktop -c:v libx264 -r 30 -preset ultrafast -tune zerolatency -crf 25 -pix_fmt yuv420p screen.mp4
--------------------------------------
изменить ориентацию видео без перекодирования (0, 90, 180, 270) 
ffmpeg -i 1.mp4 -codec copy -map_metadata 0 -metadata:s:v:0 rotate=0 0.mp4
--------------------------------------
конвертировать аудио в видео с картинкой
ffmpeg -i 1.mp3 -i 1.PNG -c copy 1.avi
```
