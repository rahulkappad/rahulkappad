const fs = require('fs');
const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

const ask = (q) => new Promise((res) => rl.question(q, res));

(async () => {
  const name = await ask('👤 Your Name: ');
  const bio = await ask('📝 Short Bio: ');
  const github = await ask('🔗 GitHub Username: ');
  const linkedin = await ask('🔗 LinkedIn URL (optional): ');
  const twitter = await ask('🔗 Twitter URL (optional): ');
  const skills = await ask('💻 Skills (comma-separated): ');

  const content = `
# 👋 Hi, I'm ${name}

${bio}

---

## 🚀 Skills
${skills.split(',').map(s => `- ${s.trim()}`).join('\n')}

---

## 📫 Connect with me:
- GitHub: [${github}](https://github.com/${github})
${linkedin ? `- LinkedIn: [${linkedin}](${linkedin})` : ''}
${twitter ? `- Twitter: [${twitter}](${twitter})` : ''}

---

![${github}'s GitHub stats](https://github-readme-stats.vercel.app/api?username=${github}&show_icons=true&theme=default)
`;

  fs.writeFileSync('README.md', content.trim());
  console.log('\n✅ README.md created successfully!');
  rl.close();
})();
