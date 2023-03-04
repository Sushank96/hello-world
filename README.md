const generatePDF = async (name)=>{
    const{ PDFDocument, rgb } = PDFLib;

    const exBytes = await fetch("./cert.pdf").then(res=>{
        return res.arrayBuffer();
        });

            //getting the fomnt from the folder
    const exFont = await fetch("./Sanchez-Regular.ttf").then(res =>{
        return res.arrayBuffer();
    });

        const pdfDoc = await PDFDocument.load(exBytes);


        pdfDoc.registerFontkit(fontkit);
        const myFont = await pdfDoc.embedFont(exFont);


        const pages = pdfDoc.getPages();
        const firstPg = pages[0]; 



        //text and location of the text cordinating with X and Y axis
    firstPg.drawText(name,{
        x: 300,
        y: 270, 
        size: 58,
        font: myFont,
        color: rgb(0.2, 0.84, 0.67),
    });




        const uri = await pdfDoc.saveAsBase64({dataUri: true});
        saveAs(uri, "Coepd.pdf", { autoBom: true }); 

        document.querySelector("#mypdf").src = uri;

};

generatePDF()




const generatePDF2 = async (date)=>{
    const{PDFDocument, rgb }= PDFLib;
    const exBytes = await fetch("./cert.pdf").then(res=>
        {return res.arrayBuffer()
        });

        const PDFDoc = await PDFDocument.load(exBytes)

        const uri = await pdfDoc.saveAsBase64({dataUri: true})

        document.querySelector("#mypdf").src = uri;

};
generatePDF2()
