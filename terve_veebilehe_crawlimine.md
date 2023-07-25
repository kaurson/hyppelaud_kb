# Kuidas tõmmata alla terve veebilehe contenet kasutades wget-i
pane faili nime lõppu .sh

wget \
     --recursive \
     --no-clobber \
     --page-requisites \
     --html-extension \
     --convert-links \
     --restrict-file-names=windows \
     https://learning.feelingstream.com/knowledgebase/ <- veebisait mida tahad crawlida
