# R-stock-price-analysis
An Interactive Visualization of Bank Sector Stock 
install.packages("quantmod")
install.packages("dygraphs")
library("quantmod");library("dygraphs")
getSymbols("BOB")    # FOR GETTING DATA OF STOCK FROM SYMBOL THAT CAN BE USED LATER ON DIRECTLY 
head(BOB,5)
price=na.omit(OHLC(BOB));head(price,5);
tail(price,5)
library(RColorBrewer)   # An library in R used for various colors pallate along with shading graphs or label 
dygraph(price,main="BOB stock price analysis")%>%dyOptions(colors = RColorBrewer::brewer.pal(4,"Dark2"))  # for making graph alongwith color or other option 
dygraph(price,main="BOB Stock price analysis")%>%
  dySeries(label = "Temp(F)",color = "Black")%>%
  dyShading(from = "2021-1-13",to="2021-12-31",color = "#FFE6E6")%>%
  dyShading(from = "2022-1-1",to="2022-10-24",color="#CCEBD6")
# Using ROC curve 
rroc=ROC(BOB[,4])
rmean=mean(rroc,na.rm=TRUE);rsd=sd(rroc,na.rm = TRUE)
dygraph(rroc,main = "BOB Share Price ")%>%
  dySeries("BOB.Close",label = "BOB")%>%
  dyShading(from = rmean-rsd,to = rmean+rsd ,axis="y")
# using candlestick 
BOB=tail(BOB,100); graph =dygraph(OHLC(BOB));dyCandlestick(graph)
getSymbols("PNB")
stocks=cbind(BOB[1:30,2:4],PNB[3951:3981,2:4])
dygraph(stocks,main = "BOB price")%>%
  dySeries(c("BOB.Low","BOB.Close","BOB.High"),label="BOB")%>%
  dySeries(c("PNB.Low","PNB.Close","PNB.High"),label="PNB")
