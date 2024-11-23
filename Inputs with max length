$().__proto__.maxLength = function(maxLength, WithContador = false) {
    if (this.is("input") || this.is("textarea")) {
        let IDParent = this.attr('id');
        let IDLabel = IDParent + "__ContadorLabel"
        let IDContador = IDParent + '__ContadorCaracteres';
        let Contador = 0;
        let LabelContador;
 
        if (WithContador) {
            if ($('head').find('#StyleContadorLabel').length == 0) {
                let Style = `<style id="StyleContadorLabel">.__ContadorLabel { font-family="Helvetica Neue"; font-size: 0.8rem;position: absolute;top: -1.25rem;right: 1.15rem;color: black; } .__ContadorCaracteres {color: gray; }</style>`;
                $('head').append(Style);
            }
            let Contador = 0;
            LabelContador = $(`<label class="__ContadorLabel"><span class="__ContadorCaracteres" id="${IDContador}">0</span><span>/</span><span>${maxLength}</span></label>`);
            this.before(LabelContador);
            LabelContador.attr("data-caracteres", Contador);
        }
        
        /* Devuelve true si hay texto seleccionado */
        function TextoSeleccionado() {
            if (window.getSelection) {
                return window.getSelection().toString().length >= 1;
            }
            else if (document.getSelection) {
                return document.getSelection().length >= 1;
            }
            else if (document.selection) {
                return document.selection.createRange().text.length >= 1;
            }
        }
 
        function ControlMaximaLongitud(e) {
            let Element = $(e.target);
 
            const allowedKeys = [
                'Backspace', 'ArrowLeft', 'ArrowRight', 'ArrowUp', 'ArrowDown', 'Delete',
                'Control', 'Meta', 'Tab', 'Home', 'End'
            ];
 
            /* Permitimos algunas teclas */
            if (allowedKeys.includes(e.key) || e.ctrlKey || e.metaKey) {
                return; 
            }           
            /* Bloqueamos las teclas si el contenido ya alcanzo la longitud maxima */
            else if (Element.val().length >= maxLength ) {
                if (!TextoSeleccionado()) e.preventDefault();
                return;
            }
        }
 
        function ForzarMaximaLongitud(event){
            let TextoCortado = $(event.target).val().slice(0, maxLength);
            if ($(event.target).val().length > maxLength) $(event.target).val(TextoCortado); 
        }
 
        function ControlContador(event) {
            let TextoCortado = $(event.target).val().slice(0, maxLength);
            Contador = TextoCortado.length;
            $(`#${IDContador}`).html(Contador);
            LabelContador.attr("data-caracteres", Contador);
        }
 
        this.on('keydown', ControlMaximaLongitud);
        this.on('input paste drop', ForzarMaximaLongitud);
        this.on('input paste drop', ControlContador);
        
    }
 
}
