from Tkinter import *
from tkMessageBox import *
from datetime import *
import time
from tkSimpleDialog import askstring


class double:
	def __init__(self):
		win = Tk()
		win.title('Connect Five')
		
		# Temp refresher
		C5Sfile = open('C:/Python27/C5_single_Move','w')
		C5Sfile.close()
		
		
		
		global referee, Bin, Blackmove, Whitemove, Bluemove, Redmove, movecount, Turn, BoardSize, Bdcolor
		
		referee = 'ABCD'

		Bin =[]

		self.TopLabel = Label(win,text ='Ctrl + Click = Black  Alt + Click = White \n Shift + Click = Blue  Shift + Ctrl + Click = Red') 
		self.TopLabel.pack()


		#Move Count
		Blackmove = Whitemove = Bluemove = Redmove = 0

		movecount = 'WAITING FOR PLAYERS'
		self.MoveLabel = Label(win, text = movecount, font = 12)
		self.MoveLabel.pack()

		#Turn Label
		Turn = "Start the game"
		self.TurnLabel = Label(win,text = Turn, font = 12)
		self.TurnLabel.pack()
		
		#Board
		if BoardSize is 'X':
			side = 900
		
		elif BoardSize is 'L':
			side = 700
		
		elif BoardSize is 'M':
			side = 550
		
		elif BoardSize is 'S':
			side = 400
			
		self.canv = Canvas(win,width = side, height = side, bg = Bdcolor, cursor = 'tcross')
		self.canv.pack()
		LINES = range(10,side,25)
		for LL in LINES:
			self.canv.create_line(10,LL,side-15,LL)
			self.canv.create_line(LL,10,LL,side-15)
	
			
		#Popup Menu
		self.menu = Menu(win,tearoff = 0)
		self.menu.add_command(label = 'Clear All',command = self.clear)
		self.menu.add_command(label = 'Chat', command = self.chat)
		self.menu.add_command(label = 'Mercy', command = self.mercy)
		
		
		self.KeyBinding()
		

		
		win.mainloop()
	
	def KeyBinding(self):
		self.canv.bind('<Control-Button-1>',self.markinput_Black)
		self.canv.bind('<Alt-Button-1>',self.markinput_White)
		self.canv.bind('<Shift-Button-1>',self.rightkey)
		self.canv.bind('<Control-Shift-Button-1>',self.rightkey)
		self.canv.bind('<Button-3>',self.popup)

	def alart(self):
		print 'warning',showwarning("Referee",'WAIT FOR YOUR TURN')

	def rightkey(self,event):
		print 'error',showerror('Referee','INVALID KEY PRESSED')

	def popup(self,event):
		self.menu.post(event.x_root, event.y_root)
		
	def chat(self):
		C5_single_chat()
		# chatwin = Tk()
		# self.chatcanv = Canvas(chatwin, width = 100, height = 100, bg='yellow')
		# self.chatcanv.pack()

	def clear(self):
		self.canv.delete('mark')	
		global Bin, Blackmove, Whitemove, Bluemove, Redmove, Turn, referee
		Blackmove = Whitemove = Bluemove = Redmove = 0
		Turn = "RESTART THE GAME"
		self.TurnLabel['text'] = Turn
		self.TurnLabel['bg'], self.TurnLabel['fg'] = 'black','gold'
		Bin =[]
		referee = 'ABCD'
		self.display()		

	'''
	def recorder(self,a):
		global Bin
		Bin.append(a)
		self.display()
		print Bin
	'''

	def clerk(self, move):
		moveN = str(move)+'\n'
		C5Sfile = open('C:/Python27/C5_single_Move','a')
		C5Sfile.write(moveN)
		C5Sfile.close()
		self.extract()

		
	def extract(self):
		global Bin
		while True:
			C5Sfile = open('C:/Python27/C5_single_Move','r')
			ff = C5Sfile.readlines()
			C5Sfile.close()
			Bin = []
			for Marks in ff:
				Bin.append(Marks[0:len(Marks)-1])
			self.display()
			self.canv.after(400)
			self.canv.update()
	
	def mercy(self):
		global Bin
		Bin = Bin[0:(len(Bin)-1)]
		
		self.display()
		
	def compiler(self,X,Y,Color):
		XcooADJ = int(25*round(float(X-10)/25)+10)
		YcooADJ = int(25*round(float(Y-10)/25)+10)
		
		Mark = str(XcooADJ) + "-" + str(YcooADJ) + "-" + Color
		self.clerk(Mark)
		
	def display(self):
		
		global Bin, Blackmove, Whitemove, Bluemove, Redmove, Turn, movecount, player
		Blackmove = Whitemove = Bluemove = Redmove = 0
		self.canv.delete('mark')
		for ee in Bin:
			bb = ee.split('-')
			Xcoo, Ycoo, color2 = int(bb[0]), int(bb[1]), bb[2]
			x1, x2, y1, y2 = (Xcoo-8), (Xcoo+8), (Ycoo-8), (Ycoo+8)
			
			if color2 == 'black':
				Blackmove += 1
				Turn = "White"
				player = P2N
				self.TurnLabel['bg'], self.TurnLabel['fg'] = 'white', 'black'
			
			elif color2 == 'white':
				Whitemove += 1
				Turn = "Black"
				player = P1N
				self.TurnLabel['bg'], self.TurnLabel['fg'] = 'black','white'
			
			self.canv.create_oval(x1,y1,x2,y2, fill = color2, tags = 'mark')

		print Bin
			
		self.TurnLabel['text'] = ('{},{}\'s turn'.format(player,Turn))
		self.MoveLabel['text'] = ('Black Move:{}   White Move:{}'.format(Blackmove,Whitemove))
			
			

	def markinput_Black(self,event):
		global referee, Turn, Blackmove
		if 'A' in referee:
			referee = 'B'
			color = 'black'
			X, Y, C = event.x, event.y, color
			self.compiler(X,Y,C)
		else:
			self.alart()
			
	def markinput_White(self,event):
		global referee, Turn, whitemove
		if 'B' in referee:
			referee = 'A'
			color = 'white'
			X, Y, C = event.x, event.y, color
			self.compiler(X,Y,C)
		else:
			self.alart()
##############################################################################

class triple(double):
	
	def KeyBinding(self):
		self.canv.bind('<Control-Button-1>',self.markinput_Black)
		self.canv.bind('<Alt-Button-1>',self.markinput_White)
		self.canv.bind('<Shift-Button-1>',self.markinput_Blue)
		self.canv.bind('<Control-Shift-Button-1>',self.rightkey)
		self.canv.bind('<Button-3>',self.popup)	
	
	def markinput_White(self,event):
		global referee, Turn, whitemove
		if 'B' in referee:
			referee = 'C'
			color = 'white'
			X, Y, C = event.x, event.y, color
			self.compiler(X,Y,C)
		else:
			self.alart()
	
	def markinput_Blue(self,event):
		global referee, Turn, Bluemove
		if 'C' in referee:
			referee = 'A'
			color = 'blue'
			X, Y, C = event.x, event.y, color
			self.compiler(X,Y,C)
		else:
			self.alart()
			
	def display(self):
		while True:
			global Bin, Blackmove, Whitemove, Bluemove, Redmove, Turn, movecount
			Blackmove = Whitemove = Bluemove = Redmove = 0
			for ee in Bin:
				bb = ee.split('-')
				Xcoo, Ycoo, color2 = int(bb[0]), int(bb[1]), bb[2]
				x1, x2, y1, y2 = (Xcoo-8), (Xcoo+8), (Ycoo-8), (Ycoo+8)
				
				if color2 == 'black':
					Blackmove += 1
					Turn = "White's Turn"
					player = P2N
					self.TurnLabel['bg'], self.TurnLabel['fg'] = 'white', 'black'
				
				elif color2 == 'white':
					Whitemove += 1
					Turn = "Blue's Turn"
					player = P3N
					self.TurnLabel['bg'], self.TurnLabel['fg'] = 'blue','white'
				
				elif color2 == 'blue':
					Bluemove += 1
					Turn = "Black's Turn"
					player = P1N
					self.TurnLabel['bg'], self.TurnLabel['fg'] = 'black','white'		

				self.canv.create_oval(x1,y1,x2,y2, fill = color2, tags = 'mark')

			print Bin
			
			self.TurnLabel['text'] = Turn
			self.MoveLabel['text'] =('Black Move:{}  White Move:{}  Blue Move:{}'.format(Blackmove,Whitemove,Bluemove))
			self.canv.after(300)
			self.canv.update()
###################################################################################		
class quad(triple):
	
	def KeyBinding(self):
		self.canv.bind('<Control-Button-1>',self.markinput_Black)
		self.canv.bind('<Alt-Button-1>',self.markinput_White)
		self.canv.bind('<Shift-Button-1>',self.markinput_Blue)
		self.canv.bind('<Control-Shift-Button-1>',self.markinput_Red)
		self.canv.bind('<Button-3>',self.popup)	
		
	def markinput_Blue(self,event):
		global referee, Turn, Bluemove
		if 'C' in referee:
			referee = 'D'
			color = 'blue'
			X, Y, C = event.x, event.y, color
			self.compiler(X,Y,C)
		else:
			self.alart()	
		
	def markinput_Red(self,event):
		global referee, Turn, Redmove
		if 'D' in referee:
			referee = 'A'
			color = 'red'
			X, Y, C = event.x, event.y, color
			self.compiler(X,Y,C)
		else:
			self.alart()
			
	def display(self):
		while True:
			global Bin, Blackmove, Whitemove, Bluemove, Redmove, Turn, movecount
			Blackmove = Whitemove = Bluemove = Redmove = 0
			for ee in Bin:
				bb = ee.split('-')
				Xcoo, Ycoo, color2 = int(bb[0]), int(bb[1]), bb[2]
				x1, x2, y1, y2 = (Xcoo-8), (Xcoo+8), (Ycoo-8), (Ycoo+8)
				
				if color2 == 'black':
					Blackmove += 1
					Turn = "white's"
					player = P1N
					self.TurnLabel['bg'], self.TurnLabel['fg'] = 'white', 'black'
				
				elif color2 == 'white':
					Whitemove += 1
					Turn = "blue's"
					player = P2N
					self.TurnLabel['bg'], self.TurnLabel['fg'] = 'blue','white'
				
				elif color2 == 'blue':
					Bluemove += 1
					Turn = "red's"
					player = P3N
					self.TurnLabel['bg'], self.TurnLabel['fg'] = 'red','white'
				
				elif color2 == 'red':
					Redmove += 1
					Turn = "black's"
					player = P4N
					self.TurnLabel['bg'], self.TurnLabel['fg'] = 'black','white'				

				self.canv.create_oval(x1,y1,x2,y2, fill = color2, tags = 'mark')

			print Bin
			
			self.TurnLabel['text'] = ('{},{} turn.'.format(player,Turn))
			self.MoveLabel['text'] = ('{} Black Move:{}   {} White Move:{} \n {} Blue Move:{}   {} Red Move:{}'.format(P1N,Blackmove,P2N,Whitemove,P3N,Bluemove,P4N,Redmove))
			self.canv.after(300)
			self.canv.update()


###################################################################################



class C5_single_chat:

	def chatpopup(self,event):
		self.chatmenu.post(event.x_root, event.y_root)

	def chatclerk_Enter(self,event):
		self.chatclerk()
		
	def chatclerk(self):
		global channel, Blabla, Chplayer
		TT1 = datetime.now().strftime('%d %H:%M:%S') 
		Chbb = Blabla.get()
		self.chatent.delete(0,END)
		Chcc = 'T' + '-' + TT1+ '-' + Chplayer+ '-' + Chbb + '\n'
		self.Chfile = open(channel,'a')
		self.Chfile.write(Chcc)
		self.Chfile.close()
		self.chatextract()
		print Chbb

	def chatreset_F5(self,event):
		self.chatreset()
		
	def chatreset(self):
		global channel, chatUserBin, chatTalkBin
		self.chreset = open(channel,'w')
		self.chreset.close()
		self.txt.delete('1.0',END)
		self.chatUserText.delete(1.0,END)
		chatUserBin = []
		chatTalkBin = []
		
		self.chatextract()

	def chatfootprint(self):
		global channel, ChLL, Chplayer
		a = 0
		while True:
			if a > 10:
				a = 0
				self.Chfile = open(channel,'a')
				fp = 'F' + '-' + 'TT1' + '-' + Chplayer + '-\n'
				self.Chfile.write(fp)
				self.Chfile.close()
				if len(ChLL) > 10:
					self.chatTextCutter()
					print 'line cut'
				else:pass
			else: 
				a += 1
			self.chatextract()
			time.sleep(0.3)
			self.txt.update()
			print 'a is',a
		
		
	def chatTextCutter(self):
		global ChLL, chatUserBin, channel
		ChRLL = ChLL[5:]
		self.Chfile = open(channel,'w')
		for ReTxt in ChRLL:
			ReTxt +'\n'
			self.Chfile.write(ReTxt)
		self.Chfile.close()
		chatUserBin = []
		self.chatUserText.delete(1.0,END)
		
	def chatextract(self):
		global channel, ChLL, user
		 
		self.Chfile = open(channel,'r')
		ChLL = self.Chfile.readlines()
		self.Chfile.close()
		for ChL in ChLL:
			frag = ChL.split('-')
			
			if frag[0] is 'T':
				chatline = frag[1] +'['+ frag[2]+'] '+ frag[3]
				if chatline in chatTalkBin:pass
				else:
					chatTalkBin.append(chatline)
					chatTalkBin.reverse()
					self.txt.delete('1.0',END)
					for LL in chatTalkBin:
						self.txt.insert(END,LL)
					chatTalkBin.reverse()
						
			elif frag[0] is 'F':
				user = frag[2]
				if user in chatUserBin:pass
				else:
					ChAnnounce = 'T' + '-' + ' ' + '-' + user+ '-' + 'has joined the Channel' + '\n'
					self.Chfile = open(channel,'a')
					self.Chfile.write(ChAnnounce)
					self.Chfile.close()
					chatUserBin.append(user)
					self.chatUserText.delete(1.0,END)
					for name in chatUserBin:
						name = name+'\n'
						self.chatUserText.insert(END,name)
			

	def RadioPro(self):
		global channel, ChRadio, chatTalkBin, chatUserBin, user
		ChAnnounce = 'T' + '-' + ' ' + '-' + user+ '-' + 'left the Channel' + '\n'
		self.Chfile = open(channel,'a')
		self.Chfile.write(ChAnnounce)
		self.Chfile.close()
		self.txt.delete('1.0',END)
		self.chatUserText.delete(1.0,END)
		if ChRadio.get() == '1':
			channel = channel1
		elif ChRadio.get() == '2':
			channel = channel2
		elif ChRadio.get() == '3':
			channel = channel3	
		chatTalkBin = []
		chatUserBin = []
		self.chatfootprint()

	def __init__(self):	
		global player, chatBin, chatUserBin, chatTalkBin, Blabla, ChRadio, channel, channel1, channel2, channel3, Chplayer
		chatwin = Tk()
		chatwin.title('Chat')

		# Player and Defualt Setting
		Chplayer = askstring('Name', 'Input your name \nex)Dodo.B')
		chatBin = []
		chatUserBin = []
		chatTalkBin = []
		a2 = 0

		# Frame 1,2,3,4	
		chfr1 = Frame(chatwin)
		chfr2 = Frame(chatwin)
		chfr3 = Frame(chatwin)
		chfr4 = Frame(chatwin)
		chfr1.grid(row =0, column = 0)
		chfr2.grid(row =1, column = 0)
		chfr3.grid(row =2, column = 0)
		chfr4.grid(row =0, column = 1, rowspan = 3)


		# Frame 1: Main text window and Scrollbar
		self.ScBar1 = Scrollbar(chfr1)
		self.ScBar1.pack(side = RIGHT, fill = Y)
		self.txt = Text(chfr1, height = 15, width = 38, bg = 'light grey',yscrollcommand = self.ScBar1.set)
		self.txt.pack()
		self.ScBar1.config(command = self.txt.yview)


		# Frame 2: Entry and Send Button

		Blabla = StringVar()
		self.chatent = Entry(chfr2, textvariable = Blabla, bg = 'light grey', width = 25)
		self.chatbut = Button(chfr2, text = "Send", command = self.chatclerk, bg = 'red', width = 5)
		self.chatent.grid(row = 0, column = 0)
		self.chatbut.grid(row = 0, column = 1)


		# Frame 3: Radio Button 1,2,3
		ChRadio = StringVar()
		self.rdB1 = Radiobutton(chfr3, variable = ChRadio, value = '1', command = self.RadioPro, text = 'channel 1')
		self.rdB2 = Radiobutton(chfr3, variable = ChRadio, value = '2', command = self.RadioPro, text = 'channel 2')
		self.rdB3 = Radiobutton(chfr3, variable = ChRadio, value = '3', command = self.RadioPro, text = 'channel 3')
		self.rdB1.grid(row =0, column =0)
		self.rdB2.grid(row =0, column =1)
		self.rdB3.grid(row =0, column =2)

		# Frame 4: User Label and Text window
		self.chatUserLabel = Label(chfr4, text = 'Current\nUsers', width = 9, height = 2)
		self.chatUserText = Text(chfr4, width = 9, height = 15, bg = 'grey')
		self.chatUserLabel.grid(row = 0, column = 0)
		self.chatUserText.grid(row = 1, column = 0)

		# Chat Popup Menu
		self.chatmenu = Menu(chfr1,tearoff = 0)
		self.chatmenu.add_command(label = 'Clear Window <F5>',command = self.chatreset)

		# Key Binding
		self.txt.bind('<Button-3>',self.chatpopup)
		self.txt.bind('<F5>',self.chatreset_F5)
		self.chatent.bind('<Return>',self.chatclerk_Enter)	
		self.chatent.bind('<F5>',self.chatreset_F5)



		# Text Channel Pilot
		standby = 'C:/Python27/C5_Single_standby'
		channel1 = 'C:/Python27/C5_Single_Channel1'
		channel2 = 'C:/Python27/C5_Single_Channel2'
		channel3 = 'C:/Python27/C5_Single_Channel3'

		standby_start = open('C:/Python27/C5_Single_standby','w')
		self.txt.insert(END,'\n\n\n		Pick a Channel')
		channel1_start = open('C:/Python27/C5_Single_Channel1','a')
		channel2_start = open('C:/Python27/C5_Single_Channel2','a')
		channel3_start = open('C:/Python27/C5_Single_Channel3','a')

		standby_start.close()
		channel1_start.close()
		channel2_start.close()
		channel3_start.close()

		channel = standby

		print("Don't forget to press \"F5\" once in a while to ease the computer")

		# Loop Triger
		self.chatfootprint()

		chatwin.mainloop()


# Preface
def PlayFor2():
	global P1N, P2N
	P1N = name1.get()
	P2N = name2.get()
	if P1N is '':
		ans = askyesno('player 1', 'continue w/o name?')
		if ans is False:
			pass
		else:
			P1N = 'player1'
			if P2N is '':
				ans = askyesno('player2', 'continue w/o name?')
				if ans is False:
					pass
				else:
					P2N = 'player2'
					double()
			else:double()		
	else:
		if P2N is '':
			ans = askyesno('player2', 'continue w/o name?')
			if ans is False:
				pass
			else:
				P2N = 'player2'
				double()
		else: double()
	
	
def PlayFor3():
	global P1N, P2N, P3N
	P1N = name1.get()
	P2N = name2.get()
	P3N = name3.get()
	if P1N is '':
		ans = askyesno('player 1', 'continue w/o name?')
		if ans is False:
			pass
		else:
			P1N = 'player1'
			if P2N is '':
				ans = askyesno('player2', 'continue w/o name?')
				if ans is False:
					pass
				else:
					P2N = 'player2'
					if P3N is '':
						ans = askyesno('player3','continue w/o name?')
						if ans is False:
							pass
						else:
							P3N = 'player3'
							triple()
					else:triple()
			else:
				if P3N is '':
						ans = askyesno('player3','continue w/o name?')
						if ans is False:
							pass
						else:
							P3N = 'player3'
							triple()
					
				else:triple()	
	else:
		if P2N is '':
				ans = askyesno('player2', 'continue w/o name?')
				if ans is False:
					pass
				else:
					P2N = 'player2'
					if P3N is '':
						ans = askyesno('player3','continue w/o name?')
						if ans is False:
							pass
						else:
							P3N = 'player3'
							triple()
					else:triple()
		else:
			if P3N is '':
				ans = askyesno('player3','continue w/o name?')
				if ans is False:
					pass
				else:
					P3N = 'player3'
					triple()
			else:triple()
	
def PlayFor4():
	global P1N, P2N, P3N, P4N
	P1N = name1.get()
	P2N = name2.get()
	P3N = name3.get()
	P4N = name4.get()
	if P1N is '':
		ans = askyesno('player 1', 'continue w/o name?')
		if ans is False:
			pass
		else:
			P1N = 'player1'
			if P2N is '':
				ans = askyesno('player2', 'continue w/o name?')
				if ans is False:
					pass
				else:
					P2N = 'player2'
					if P3N is '':
						ans = askyesno('player3','continue w/o name?')
						if ans is False:
							pass
						else:
							P3N = 'player3'
							if P4N is '':
								ans = askyesno('player4','continue w/o name?')
								if ans is False:
									pass
								else:
									P4N = 'player4'
									quad()
							else:quad()
					else:
						if P4N is '':
							ans = askyesno('player4','continue w/o name?')
							if ans is False:
								pass
							else:
								P4N = 'player4'
								quad()
						else:quad()
			else:
				if P3N is '':
					ans = askyesno('player3','continue w/o name?')
					if ans is False:
						pass
					else:
						P3N = 'player3'
						if P4N is '':
							ans = askyesno('player4','continue w/o name?')
							if ans is False:
								pass
							else:
								P4N = 'player4'
								quad()
						else:quad()
				else:
					if P4N is '':
						ans = askyesno('player4','continue w/o name?')
						if ans is False:
							pass
						else:
							P4N = 'player4'
							quad()
					else:quad()
	else:
		if P2N is '':
			ans = askyesno('player2', 'continue w/o name?')
			if ans is False:
				pass
			else:
				P2N = 'player2'
				if P3N is '':
					ans = askyesno('player3','continue w/o name?')
					if ans is False:
						pass
					else:
						P3N = 'player3'
						if P4N is '':
							ans = askyesno('player4','continue w/o name?')
							if ans is False:
								pass
							else:
								P4N = 'player4'
								quad()
						else:quad()
				else:
					if P4N is '':
						ans = askyesno('player4','continue w/o name?')
						if ans is False:
							pass
						else:
							P4N = 'player4'
							quad()
					else:quad()
		else:
			if P3N is '':
				ans = askyesno('player3','continue w/o name?')
				if ans is False:
					pass
				else:
					P3N = 'player3'
					if P4N is '':
						ans = askyesno('player4','continue w/o name?')
						if ans is False:
							pass
						else:
							P4N = 'player4'
							quad()
					else:quad()
			else:
				if P4N is '':
					ans = askyesno('player4','continue w/o name?')
					if ans is False:
						pass
					else:
						P4N = 'player4'
						quad()
				else:quad()
			

def BoardRadio():
	global BoardSize
	if Bsize.get() is 'X':
		BoardSize = 'X'
	
	elif Bsize.get() is 'L':
		BoardSize = 'L'

	elif Bsize.get() is 'M':
		BoardSize = 'M'

	elif Bsize.get() is 'S':
		BoardSize = 'S'

		
def BoardColorRadio():
	global Bdcolor
	if Bcolor.get() is 'B':
		Bdcolor = '#aa6611'
	elif Bcolor.get() is 'G':
		Bdcolor = 'grey'


Frontpage = Tk()
Frontpage.title('Connect Five. DodoBird')

fr1 = Frame(Frontpage)
fr2 = Frame(Frontpage)
fr3 = Frame(Frontpage)
fr4 = Frame(Frontpage)
fr5 = Frame(Frontpage)
fr6 = Frame(Frontpage)
fr7 = Frame(Frontpage)
fr8 = Frame(Frontpage)
fr9 = Frame(Frontpage)

Title_Label = Label(fr9, text = 'Connect Dots	\n	Single PC ver.', width = 18, font = 'aharoni 12')
Title_Label.pack()

FrontLabel = Label(fr1, text = 'How many players?', width = 25)
NameLabel = Label(fr4, text = 'Your name please\nex) Dodo.B')
PlayerNumButton2 = Button(fr2, text = 'Two', command = PlayFor2)
PlayerNumButton3 = Button(fr2, text = 'Three', command = PlayFor3)
PlayerNumButton4 = Button(fr2, text = 'Four', command = PlayFor4)

name1 = StringVar()
name2 = StringVar()
name3 = StringVar()
name4 = StringVar()
Name1ent = Entry(fr3,textvariable = name1, width = 15, bg = 'grey')
Name2ent = Entry(fr3,textvariable = name2, width = 15, bg = 'grey')
Name3ent = Entry(fr3,textvariable = name3, width = 15, bg = 'grey')
Name4ent = Entry(fr3,textvariable = name4, width = 15, bg = 'grey')
Name1Lab = Label(fr3,text = 'Player1', bg = 'black', fg = 'white')
Name2Lab = Label(fr3,text = 'Player2', bg = 'white', fg = 'black')
Name3Lab = Label(fr3,text = 'Player3', bg = '#0033dd', fg = 'white')
Name4Lab = Label(fr3,text = 'Player4', bg = '#991111', fg = 'white')


FrontLabel.pack()
PlayerNumButton2.grid(row =0, column = 0)
PlayerNumButton3.grid(row =0, column = 1)
PlayerNumButton4.grid(row =0, column = 2)
Name1ent.grid(row =0, column = 1)
Name2ent.grid(row =1, column = 1)
Name3ent.grid(row =2, column = 1)
Name4ent.grid(row =3, column = 1)

Name1Lab.grid(row =0, column = 0)
Name2Lab.grid(row =1, column = 0)
Name3Lab.grid(row =2, column = 0)
Name4Lab.grid(row =3, column = 0)
NameLabel.pack()

Bsize = StringVar()
BoardSize = Label(fr5, text = 'Board Size', width = 25)
BS_XL = Radiobutton(fr6, text = 'XL', variable = Bsize, value = 'X' ,command = BoardRadio)
BS_L = Radiobutton(fr6, text = 'LG', variable = Bsize, value = 'L' ,command = BoardRadio)
BS_M = Radiobutton(fr6, text = 'MD', variable = Bsize, value = 'M' ,command = BoardRadio)
BS_S = Radiobutton(fr6, text = 'SM', variable = Bsize, value = 'S' ,command = BoardRadio)

BoardSize.grid(column = 0, row = 0)
BS_XL.grid(column = 3, row = 0)
BS_L.grid(column = 2, row = 0)
BS_M.grid(column = 1, row = 0)
BS_S.grid(column = 0, row = 0)

Bcolor = StringVar()
BoardColor = Label(fr7, text = 'Choose Your Board', width = 20, font = 'arial 10')
BC_B = Radiobutton(fr8, text = 'Wood', variable = Bcolor, value = 'B' ,command = BoardColorRadio)
BC_G = Radiobutton(fr8, text = 'Stone', variable = Bcolor, value = 'G' ,command = BoardColorRadio)
BoardColor.pack()
BC_B.grid(column = 0, row = 0)
BC_G.grid(column = 1, row = 0)

fr9.pack()
fr4.pack()
fr3.pack()
fr5.pack()
fr6.pack()
fr7.pack()
fr8.pack()
fr1.pack()
fr2.pack()

Frontpage.mainloop()

'''	
Frontpage = Tk()

fr1 = Frame(Frontpage)
fr2 = Frame(Frontpage)
FrontLabel = Label(fr1, text = 'How many players?', width = 25)
PlayerNumButton2 = Button(fr2, text = 'Two', command = PlayFor2)
PlayerNumButton3 = Button(fr2, text = 'Three', command = PlayFor3)
PlayerNumButton4 = Button(fr2, text = 'Four', command = PlayFor4)
fr1.pack()
fr2.pack()
FrontLabel.pack()
PlayerNumButton2.grid(row =0, column = 0)
PlayerNumButton3.grid(row =0, column = 1)
PlayerNumButton4.grid(row =0, column = 2)

Frontpage.mainloop()

'''




'''
# Multi Ver.

Reset = open("C:/Python27/C5Coo.txt","w")
Reset.close()


	
def clerk(move):
	ww = open('C:/Python27/C5Coo.txt','a')
	ww.write(str(move))
	ww.wrtie('\n')
	ww.close()	
	
def extract():
	global Bin
	OO = open('C:/Python27/C5Coo.txt','r')
	ff = OO.readlines()
	OO.close()
	for PP in ff:
		Bin.append(PP[0:len(PP)-1])
	return Bin
	display()
'''

	
