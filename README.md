import React, { useEffect, useState } from "react";
import { motion, useAnimation } from "framer-motion";
import { useInView } from "react-intersection-observer";

export default function SiteMatheusTeodoro() {
  const fadeInUp = {
    hidden: { opacity: 0, y: 40 },
    visible: (i) => ({
      opacity: 1,
      y: 0,
      transition: { delay: i * 0.2, duration: 0.7, ease: "easeOut" },
    }),
  };

  const Section = ({ id, title, children }) => {
    const controls = useAnimation();
    const [ref, inView] = useInView({ threshold: 0.2 });

    useEffect(() => {
      if (inView) controls.start("visible");
    }, [controls, inView]);

    return (
      <motion.section
        id={id}
        ref={ref}
        initial="hidden"
        animate={controls}
        variants={fadeInUp}
        className="scroll-mt-20"
      >
        <h3 className="text-2xl font-semibold mb-4 text-blue-800">{title}</h3>
        {children}
      </motion.section>
    );
  };

  // Efeito de fade contínuo no fundo
  const [scrollY, setScrollY] = useState(0);
  useEffect(() => {
    const handleScroll = () => setScrollY(window.scrollY);
    window.addEventListener("scroll", handleScroll);
    return () => window.removeEventListener("scroll", handleScroll);
  }, []);

  const bgOpacity = Math.min(0.5 + scrollY / 1500, 1);

  return (
    <motion.div
      className="min-h-screen bg-[url('https://www.transparenttextures.com/patterns/cubes.png')] text-gray-800 antialiased transition-all duration-500"
      style={{ backgroundColor: `rgba(255,255,255,${bgOpacity})` }}
    >
      <header className="bg-white/80 backdrop-blur sticky top-0 z-40 border-b border-gray-200 shadow-sm">
        <div className="max-w-4xl mx-auto px-6 py-4 flex items-center justify-between">
          <motion.div initial="hidden" animate="visible" variants={fadeInUp} className="flex items-center gap-4">
            <div className="w-12 h-12 rounded-full bg-gradient-to-br from-blue-900 to-blue-700 flex items-center justify-center text-white font-semibold shadow-md">MS</div>
            <div>
              <h1 className="text-lg font-semibold text-gray-900">Matheus Serafim Teodoro</h1>
              <p className="text-sm text-gray-500">Analista de Inovação</p>
            </div>
          </motion.div>
          <motion.nav initial="hidden" animate="visible" variants={fadeInUp} className="hidden md:flex gap-6 text-sm text-gray-600">
            <a href="#about" className="hover:text-blue-700 transition">Sobre</a>
            <a href="#experience" className="hover:text-blue-700 transition">Experiência</a>
            <a href="#education" className="hover:text-blue-700 transition">Educação</a>
            <a href="#skills" className="hover:text-blue-700 transition">Habilidades</a>
            <a href="#contact" className="hover:text-blue-700 transition">Contato</a>
          </motion.nav>
        </div>
      </header>

      <main className="max-w-4xl mx-auto px-6 py-12 space-y-16">
        <Section id="hero" title="">
          <div className="grid grid-cols-1 md:grid-cols-3 gap-8 items-center">
            <div className="md:col-span-2">
              <h2 className="text-4xl font-extrabold mb-3 text-blue-800">Olá, eu sou o Matheus 👋</h2>
              <p className="text-lg text-gray-700 mb-4 leading-relaxed">Analista de Inovação com experiência em open innovation, coordenação de programas de inovação, articulação com ecossistemas (SEBRAE) e organização de hackathons. Tenho histórico de implementar culturas de inovação organizacionais e conectar soluções externas às necessidades de negócio.</p>
              <div className="flex gap-3 mt-4">
                <motion.a whileHover={{ scale: 1.05 }} href="#contact" className="inline-block bg-blue-900 text-white px-5 py-3 rounded-lg shadow hover:bg-blue-800 transition">Entrar em contato</motion.a>
                <motion.a whileHover={{ scale: 1.05 }} href="https://www.linkedin.com/in/msteodoro" target="_blank" rel="noreferrer" className="inline-block border border-blue-800 text-blue-900 px-5 py-3 rounded-lg hover:bg-blue-100 transition">LinkedIn</motion.a>
              </div>
            </div>

            <motion.aside whileHover={{ scale: 1.05 }} className="flex flex-col items-center gap-4">
              <div className="w-44 h-44 rounded-xl bg-blue-50 flex items-center justify-center text-3xl font-bold text-blue-900 border border-blue-200 shadow-sm">MS</div>
              <div className="text-center">
                <p className="text-sm text-gray-500">Uberaba - MG</p>
                <p className="text-sm text-gray-500">(34) 9 9111-6230</p>
                <p className="text-sm text-gray-500">serafimmatheus14@gmail.com</p>
              </div>
            </motion.aside>
          </div>
        </Section>

        {/* Outras seções mantêm o mesmo conteúdo */}
      </main>

      <footer className="border-t border-gray-200 bg-white/70 backdrop-blur-sm">
        <motion.div initial="hidden" animate="visible" variants={fadeInUp} className="max-w-4xl mx-auto px-6 py-6 text-sm text-center text-gray-600">
          © {new Date().getFullYear()} Matheus Serafim Teodoro — Desenvolvido por você | Portfólio
        </motion.div>
      </footer>
    </motion.div>
  );
}
