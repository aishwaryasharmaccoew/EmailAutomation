'''
Created on Nov 3, 2016

@author: admin
'''

import getpass
import smtplib
import email
import os
from email.mime.multipart import MIMEMultipart
from email.utils import COMMASPACE
from email.mime.base import MIMEBase
from email.parser import Parser
from email.mime.image import MIMEImage
from email.mime.text import MIMEText
from email.mime.audio import MIMEAudio
import mimetypes
from email.mime.application import MIMEApplication
from pip._vendor.distlib.compat import raw_input
import time

def sendfunc(accno,email_id,user,password,fromaddr,sub,path_ps,Body,extenof):
    
    server = smtplib.SMTP()
    host ='smtp.gmail.com'
    port = 587
    server.connect(host,port) 
    server.ehlo()
    server.starttls()
    

    server.login(user, password)
    
    tolist =email_id.split()
    
    msg = MIMEMultipart()
    msg['From'] = fromaddr
    msg['To'] = email.utils.COMMASPACE.join(tolist)
    msg['Subject'] = sub
    msg.attach(MIMEText(Body))
    msg.attach(MIMEText('\nsent by BSNL Pune \n Regards AOCDR \n Landline: 02024432526', 'plain')) 
    filename =path_ps+"\\"+accno+extenof
    try:
        f = open(filename,'rb')
    except (OSError,IOError) as e:
        print (".ps file for account no "+accno+" is unavailable !!!")
        return
    ctype, encoding = mimetypes.guess_type(filename)
     

    if ctype is None or encoding is not None:
        ctype = 'application/octet-stream'
    maintype, subtype = ctype.split('/', 1)
    if maintype == 'text':
        part = MIMEText(f.read(), _subtype=subtype)
    elif maintype == 'image':
        part = MIMEImage(f.read(), _subtype=subtype)
    elif maintype == 'audio':
        part = MIMEAudio(f.read(), _subtype=subtype)
    elif maintype == 'application':
        part= MIMEApplication(f.read(), _subtype = "ps")		#make _subtype as pdf for pdfs
    else:
        part = MIMEBase(maintype, subtype)
        msg.set_payload(f.read())
    part.add_header('Content-Disposition', 'attachment; filename="%s"' % os.path.basename(filename))
    msg.attach(part)
    f.close()
    server.sendmail(user,tolist,msg.as_string())
    server.quit()
    string="Sent mail to "+accno+" :  "+email_id+" Time :"+time.ctime()+"\n"
    sentfile.write(string)


user=raw_input('Enter sender id:')
print ('Enter sender password :')

password = getpass.getpass()
fromaddr = raw_input('Send mail by the name of: ')
sub = raw_input('Subject: ')    
body=raw_input('Body: ')
ch=1
while(ch):
    ch=0
    filepath=raw_input("Enter path of csv file:")
    try:
        myfile=open(filepath)
    except (OSError,IOError) as e :
        print ("Wrong Path for csv file !!!")
        ch=1
    
path_ps=raw_input("Enter path of file to attach file:")
extenof=raw_input("Enter extension of file to attach file:")

sendpath=path_ps+"\sentids.txt"
sentfile=open(sendpath, 'w')
sentfile.write("Emails sent to ids: \n")
li=list()
for line in myfile.readlines():
    print (line)
    inp=line.split(',')
    if inp[0].isdigit():
        
        if(inp[2].find("@")!= -1):
            sendfunc(inp[0],inp[2],user,password,fromaddr,sub,path_ps,body,extenof)
            
        else:
            li.append(inp[0])
            continue
        
    else:
        continue
myfile.close()
print ("\n The email ids are not provided for these account numbers :\n")
for i in range(int(len(li))):
    print (li[i])
sentfile.close()



