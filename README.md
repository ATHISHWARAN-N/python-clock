# python-clock





import smtplib
from email.message import EmailMessage
import time
from plyer import notification
import tkinter as Tkinter
from datetime import datetime
counter = 66600
running = False

a=int(input("To use stopwatch enter 1 \nTo set a reminder enter 2  :"))
if a==1:
    def counter_label(label):
      def count():
        if running:
            global counter
  
           
            if counter==66600:           
                display="Starting..."
            else:
                tt = datetime.fromtimestamp(counter)
                string = tt.strftime("%H:%M:%S")
                display=string
  
            label['text']=display  
  
       
            label.after(1000, count)
            counter += 1
  
    
      count()    
  

    def Start(label):
      global running
      running=True
      counter_label(label)
      start['state']='disabled'
      stop['state']='normal'
      reset['state']='normal'
  

    def Stop():
      global running
      start['state']='normal'
      stop['state']='disabled'
      reset['state']='normal'
      running = False
  

    def Reset(label):
      global counter
      counter=66600
  
    
      if running==False:     
        reset['state']='disabled'
        label['text']='Welcome!'
  
    
      else:              
        label['text']='Starting...'
root = Tkinter.Tk()
    root.title("Stopwatch")
  

    root.minsize(width=250, height=70)
    label = Tkinter.Label(root, text="Welcome!", fg="black", font="Verdana 30 bold")
    label.pack()
    f = Tkinter.Frame(root)
    start = Tkinter.Button(f, text='Start', width=6, command=lambda:Start(label))
    stop = Tkinter.Button(f, text='Stop',width=6,state='disabled', command=Stop)
    reset = Tkinter.Button(f, text='Reset',width=6, state='disabled', command=lambda:Reset(label))
    f.pack(anchor = 'center',pady=5)
    start.pack(side="left")
    stop.pack(side ="left")
    reset.pack(side="left")
    root.mainloop()
else:
    start=int( input("When do you want to be reminded?"))
    title=input("What do you want to be reminded about?")
    message=input("Extra information?")
    c=input("Enter the email address:")
t="You have a reminder" + "  " + title + " " + "in" + " 5 minutes "
           
        

    def email_alert(subject, body, to):
       msg= EmailMessage()
       msg.set_content(body)
       msg['subject'] = subject
       msg['to'] = to
    
       user = "Enter your Email ID"
       msg['from'] = user
       password = "Enter your password"
    
       server = smtplib.SMTP("smtp.gmail.com", 587)
       server.starttls()
       server.login(user,password)
       server.send_message(msg)

       server.quit()



if __name__ == '__main__':
    while True:
        time.sleep(start-300)
        email_alert(t, message, c)
        print("The message had been sent successfully")
        break
    

    
    
if __name__ == "__main__":
    while True:
            time.sleep(start)
            notification.notify(
            title = title,
            message = message,
            app_icon = "D:\icons\clock.ico",
            
            timeout=100
            
            )
            break
