// name and the amount of the sale.
// Sales of new and used cars are kept in separate files,
// sorted by salesperson ID number.
// Management has requested a merged file so that
// all of a salespersonís sales (both new and used cars)
// are displayed together. The following code is intended
// to merge the files.

start
   Declarations
      string newSalesperson
      num newAmount
      string usedSalesperson
      num usedAmount
      string bothAtEof = "N"
      string HIGH_NAME = "ZZZZZ"
      InputFile newSales
      InputFile usedSales
      OutputFile allSales
   getReady()
   while bothAtEof = "N"
      detailLoop()
   endwhile
   finish()
stop 

getReady()
   open newSales "NewSales.dat"
   open usedSales "UsedSales.dat"
   open allSales "AllSales.dat"

   input newSalesperson, newAmount from newSales
   input usedSalesperson, usedAmount from usedSales
   return

detailLoop()
   if newSalesperson < usedSalesperson then
      output newSalesperson, newAmount to allSales
      input newSalesperson, newAmount from newSales
      if eof then
         newSalesperson = HIGH_NAME
      endif
   else
      output usedSalesperson, usedAmount to allSales
      input usedSalesperson, usedAmount from usedSales
      if eof then
         usedSalesperson = HIGH_NAME
      endif
   endif
   if newSalesperson = HIGH_NAME AND usedSalesperson = HIGH_NAME then
      bothAtEof = "Y"
   endif
   return

finish()
   close newSales
   close usedSales
   close allSales
   return
