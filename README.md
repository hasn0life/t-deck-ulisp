# t-deck-ulisp
Attempt at getting ulisp running on the [Lilygo T-Deck](https://github.com/Xinyuan-LilyGO/T-Deck) 

# notes
The [T-Deck repo](https://github.com/Xinyuan-LilyGO/T-Deck)  contains instructions for how to upload code with the arduino IDE  

I used the [Arduino gfx](https://github.com/moononournation/Arduino_GFX) library instead of the adafruit one because the T-Deck repo examples had it working.  

Note that the I2C port needs to be routed to pins SDA -> 18 and SCL -> 8
I have routed them for the Wire1 port but not for the default port. To use these functions uncomment line 2395

# ulisp functions for screen and keyboard so far

```
;; read a key from the keyboard
(defun get ()
  (with-i2c (str #x55 1) 
      (code-char (read-byte str))))

;; color stuff
(defun rgb (r g b)   (logior (ash (logand r #xf8) 8) (ash (logand g #xfc) 3) (ash b -3)))
     
(defvar white (rgb 0 0 0))

(defvar blue (rgb 255 127 0))

;; print a string on screen
(defun print-string (txt size)
	(let ((len (length txt))
		 (_ (fill-screen)))
		(dotimes (i len)
			(draw-char (* (* size 6) i) 10 (char txt i) blue white size)))
	txt)

;; recursive loop for getting characters from the keyboard and putting them on screen
(defun getline (txt ch) 
(cond 
((equal #\Return ch) (return txt))
((equal #\Backspace ch) (getline (subseq txt 0 (- (length txt) 1)) nil))
((equal #\Null ch) (getline txt (get)))
((equal nil ch) (getline (print-string txt 2) (get)))
(t (getline (print-string (concatenate 'string txt (string ch)) 2) (get)))))

;; getline call example
(getline "" (get))

```
