# SMS-Text-Message-Testing
This line of code is put together to send SMS text message via Nexmo API platform

#!/usr/bin/python
#-----------------------------------
# Send SMS Text Message
#
# Author : Bobby Tebola
# Site   : http://rest.nexmo.com/sms/json
# Date   : 15/01/2015
#
# Requires account with Nexmo
# http://www.nexmo.com
#
#-----------------------------------

# Import required libraries
import urllib      # URL functions
import urllib2     # URL functions

# Define your message
message = 'Test message sent from my Raspberry Pi'

# Set your username and sender name.
# Sender name must alphanumeric and 
# between 3 and 11 characters in length.
username = 'bobbytebola@gmail.com'
sender = 'Bobbyteb'

# Your unique hash is available from the docs page
# https://control.nexmon.com/docs/
hash = '1234567890abcdefghijklmnopqrstuvwxyz1234'

# Set the phone number you wish to send
# message to.
# The first 2 digits are the country code.
# 44 is the country code for the UK
# Multiple numbers can be specified if required
# e.g. numbers = ('447xxx123456','447xxx654321')
numbers = ('447717259369')

# Set flag to 1 to simulate sending
# This saves your credits while you are
# testing your code.
# To send real message set this flag to 0
test_flag = 1

#-----------------------------------
# No need to edit anything below this line
#-----------------------------------

values = {'test'    : test_flag,
          'uname'   : username,
          'hash'    : hash,
          'message' : message,
          'from'    : sender,
          'selectednums' : numbers }

url = 'http://www.nexmo.com/sendsmspost.php'

postdata = urllib.urlencode(values)
req = urllib2.Request(url, postdata)

print 'Attempt to send SMS ...'

try:
  response = urllib2.urlopen(req)
  response_url = response.geturl()
  if response_url==url:
    print 'SMS sent!'
except urllib2.URLError, e:
  print 'Send failed!'
  print e.reason
